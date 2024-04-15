pipeline{
    agent { label 'slave1' }
   environment {     
        DOCKERHUB_CREDENTIALS= credentials('docker-hub')     
    }
    stages {
      stage ('Checkout') {
        steps {
            sh 'rm -rf hello-world-war'            
            sh 'git clone https://github.com/Nethravathi-R/hello-world-war.git'      
          
              }
      }
        stage ('Build') {
        steps {
            sh 'echo "inside build"'
            dir("hello-world-war") {
                sh 'echo "inside dir"'
                sh 'docker build -t tomcat-fiel:${BUILD_NUMBER} .'
            }            
          }
        }
             
        // stage ('Deploy'){
        //     steps {
        //        sh 'docker rm -f tomcat-war'
        //        sh 'docker run -d -p 8082:8080 --name tomcat-war tomcat-war:1.0'                
        //     }
        // }


        
        stage('Login to Docker Hub'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR  --password-stdin'
                echo 'Login Completed'
            }
        }
        stage('Push  Image to Docker Hub'){
              steps{
                  sh "docker tag tomcat-file:${BUILD_NUMBER} Nethravathi/master-slave:${BUILD_NUMBER}"
                  sh "docker push Nethravathi/master-slave:${BUILD_NUMBER}"
                  echo "Image pushing completed.."
              }
        }
        stage('Pull and Deploy'){
            parallel{
                stage('Deploy t node1') {
                    agent any
                    steps {
                        
                        sh "docker pull Nethravathi/master-slave1:${BUILD_NUMMBER}"
                        sh "docker run -d --name my_container_1 -p 8085:8080 Nethravathi/master-slave:${BUILD_NUMBER}"
                       }
                  }            
                stage ('Deploy to slave1'){
                    agent {label 'slave1'}
                steps {
                        sh "docker pull Nethravathi/master-slave1:${BUILD_NUMBER}"
                        sh "docker run -d --name my_container_2 -p 8086:8080 Nethravathi/master-slave:${BUILD_NUMBER}"
                      }
                 }
             }
        }
    }
}         
