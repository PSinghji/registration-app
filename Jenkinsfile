Pipeline{
  agent{ labels 'Jenkins-Agent'}
  tools{
         jdk 'Java17'
         maven 'Maven3'
  }
  stages{
    stage("Cleanup Workshop"){
       steps{
           CleanWs()
       }
    }  
    stage("Checkout from SCM"){
       steps{
           git(
            branch: 'main', 
            credentialsId: 'github', 
            url: 'https://github.com/PSinghji/registration-app.git'
        )
       }
    }
  stage("Test Application"){
       steps{
           sh "mvn test"
       }
    }
  stage("Test Application"){
       steps{
           sh "mvn test"
       }
    }
  }
}
