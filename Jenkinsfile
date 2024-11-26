pipeline {
    agent { label 'Jenkins-Agent' }
    
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    
    stages {
        stage('Cleanup Workshop') {
            steps {
                cleanWs()  // Corrected the method name to lowercase
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
    }
}
