pipeline {
    agent linuxslave1
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
        withDockerRegistry([ credentialsId: "dockerHub", url: "skcnetworknutsnodejstestrepo" ]) {
          sh  'docker push skcnetworknutsnodejstestrepo/nginxtest:latest'
          sh  'docker push skcnetworknutsnodejstestrepo/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 skcnetworknutsnodejstestrepo/nginxtest"
 
            }
        }
 
    }
}