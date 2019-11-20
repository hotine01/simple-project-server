pipeline {
    agent any   
	 stages {
        stage('Test') {
            steps {
                   echo "Test"
                }
            }
        stage('Build') {
            steps {
                    sh 'mvn package -DskipTests'
                    sh 'docker build -t="hotine01/simple-project-server:latest" .'
                }
            }
        stage('Deploy') {
            steps {
                    sh 'docker push hotine01/simple-project-server:latest'
            }
        }   
     stage('Testing Environment') {
            steps {
                echo "hello"
            }
        }
      stage('Staging') {
            steps {
                echo "hello"
            }
        }
      stage('Production') {
            steps {
               when {
		expression {
		env.feature-addfail=='master'
		}
			}
	steps{
		echo 'production'
	}
            }
        }
    }
}
