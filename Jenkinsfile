pipeline {
    agent {
            docker { image 'maven:3.8.1-adoptopenjdk-11' }
            }
    
    stages { 	
	stage('Example Build') {
		environment {
                  HOME="."
                }
            steps {
                sh 'mvn -B clean verify'
            }
        }    
        stage('Build Jar') {
		 environment {
                  HOME="."
                }
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
		 environment {
                  HOME="."
                }
            steps {
                script {
                	app = docker.build("vinsdocker/containertest")
                }
            }
        }
        stage('Push Image') {
		 environment {
                  HOME="."
                }
            steps {
                script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        	app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
                }
            }
        }        
    }
}
