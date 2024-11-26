pipeline {
    agent { label 'Jenkins-Agent' }
    
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    environment {
	    APP_NAME = "register-app-pipeline"
            RELEASE = "1.0.0"
            DOCKER_USER = "pady1989"
            DOCKER_PASS = 'dockerhub'
            IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
	    JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")
    }
    
    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs() // Corrected case for cleanWs()
            }
        }

        stage('Checkout from SCM') {
            steps {
                git(
                    branch: 'main', 
                    credentialsId: 'github', 
                    url: 'https://github.com/PSinghji/registration-app.git'
                )
            }
        }

        stage('Test Application') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube-server') { 
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                    script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
                }
            }
        }
    }
}
