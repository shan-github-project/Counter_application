pipeline{

    agent any 
    environment{
            VERSION = "${env.BUILD_ID}"
    }

    stages{

        stage('Git Checkout'){
           
            steps{

                script{
                 
                 git branch: 'main', url: 'https://github.com/shan-github-project/Counter_application.git'

                }
            }
        }
        stage('Unit Test'){

             steps{

              script{
                   
                   sh 'mvn test'

                }
             }
        }
        stage('Integration Test'){

             steps{

              script{
                   
                   sh 'mvn verify -DskipUnitTests'

                }
             }
        }
        stage('Static Code Analysis'){

             steps{

              script{
                   
                  withSonarQubeEnv(credentialsId: 'sonar-token') {
                     
                     sh 'mvn clean package sonar:sonar'
                  }
                }
             }
        }
        stage('Quality Gate status Check'){

             steps{

              script{
                   
                   waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'

                }
             }
        }
        stage('Maven Build'){

             steps{

              script{
                   
                   sh 'mvn clean install'

                }
             }
        }
     //    stage('Docker image Building'){

     //         steps{

     //          script{
                   
     //               sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
     //               sh 'docker image tag $JOB_NAME:v1.$BUILD_ID zeeshan30/$JOB_NAME:v1.$BUILD_ID'
     //               sh 'docker image tag $JOB_NAME:v1.$BUILD_ID zeeshan30/$JOB_NAME:latest'

     //            }
     //         }
     //    }
     //    stage('Docker image push'){

     //         steps{

     //          script{
     //               withCredentials([string(credentialsId: 'dockerhub_passwd', variable: 'dockerhub_passwd')]) {
                     
     //                 sh 'docker login -u zeeshan30 -p ${dockerhub_passwd}'
     //                 sh 'docker image push zeeshan30/$JOB_NAME:v1.$BUILD_ID'
     //                 sh 'docker image push zeeshan30/$JOB_NAME:latest'
     //              }
     //            }
     //         }
     //    }  
     
         stage('docker build & push to nexus repo'){

              steps{

               script{
                   withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus-credential')]) {

                   sh '''
                      docker build -t 18.233.169.244:8083/springapp:

                   '''
                   
                   }

                }
             }
         }

    }
}

// squ_531616e45ae941db981c0e09f5721d0ca515e4d4