pipeline {
    agent any
	environment {
    VERSION = readMavenPom().getVersion()
	}   
	stages {
	stage("version"){
		steps{
		echo "${VERSION}"
	}
	}
        stage('Testing') {
            steps {
                sh 'mvn test -Dtest=ControllerAndServiceSuite'
                sh 'mvn test -Dtest=IntegrationSuite'
            }
        }
        stage('Build') {
            steps {
                echo "Build"
                sh 'mvn package -DskipTests'
                sh 'docker build -t="hotine01/simple-project-server:${VERSION}" .'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy"
                sh 'docker push hotine01/simple-project-server:${VERSION}'
            }
        }
        stage('Testing Environment') {
            steps {
                echo "hello"
            }
        }
        stage('Staging') {
            when {
		expression{
		env.BRANCH_NAME=="developer"
		}
            }
	steps{	
		echo "hello"
		}
        }
        stage('Production') {
            when{
                expression{
                    env.BRANCH_NAME=="master"
                }
            }
            steps {
                echo "hello"
            }
        }  
	}
}
