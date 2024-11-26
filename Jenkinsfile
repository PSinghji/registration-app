pipeline {
    agent { label 'Jenkins-Agent' }
    
    tools {
        jdk 'Java17'
        maven 'Maven3'
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
                withSonarQubeEnv('jenkins-sonarqube-token') { 
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
