pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                sh 'docker tag nginxtest skcnetworknutsnodejstestrepo/nginxtest:latest'
                sh 'docker tag nginxtest skcnetworknutsnodejstestrepo/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "skcnetworknuts/nodejstestrepo" ]) {
          sh  'docker push skcnetworknuts/nodejstestrepo/nginxtest:latest'
          sh  'docker push skcnetworknuts/nodejstestrepo/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 skcnetworknuts/nodejstestrepo/nginxtest"
 
            }
        }
 
    }
}