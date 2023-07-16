pipeline {
  agent any
  tools {
    maven '3.6.3'
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage ('image') {
      steps {
       checkout scm
         echo 'Starting to build docker image'
         
         

                script {
                    def customImage = docker.build("prasannagundavarapu/banking")
                    
                    withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ]) {
                      sh 'docker login -u prasannagundavarapu -p maruthi@12345'
                      sh 'docker push prasannagundavarapu/banking'
             }
                    
                }
      }
    }
  }
}


