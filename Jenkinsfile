pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'

   }

    stages {
            stage('SonarQube') {
             steps {
                withSonarQubeEnv('sonar') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Microservice_Deployment -Dsonar.ProjectName=Microservice_Deployment -Dsonar.java.binaries=.'''
                }
            }
        }
            stage('adservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir('/var/lib/jenkins/workspace/Microservice_Deployment/src/adservice/') {
                        sh "docker build -t tkibnyusuf/adservice:latest ."
                        sh "docker push tkibnyusuf/adservice:latest"
                        sh "docker rmi tkibnyusuf/adservice:latest"
                    }
                }
            }
        }
            }
            stage('cartservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/cartservice/src/") {
                        sh "docker build -t tkibnyusuf/cartservice:latest ."
                        sh "docker push tkibnyusuf/cartservice:latest"
                        sh "docker rmi tkibnyusuf/cartservice:latest"
                    }
                }
            }
        }
       }
            stage('checkoutservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/checkoutservice/") {
                        sh "docker build -t tkibnyusuf/checkoutservice:latest ."
                        sh "docker push tkibnyusuf/checkoutservice:latest"
                        sh "docker rmi tkibnyusuf/checkoutservice:latest"
                    }
                }
            }
        }
            }
            stage('currencyservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/currencyservice/") {
                        sh "docker build -t tkibnyusuf/currencyservice:latest ."
                        sh "docker push tkibnyusuf/currencyservice:latest"
                        sh "docker rmi tkibnyusuf/currencyservice:latest"
                    }
                }
            }
        }

            }
            stage('emailservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/emailservice/") {
                        sh "docker build -t tkibnyusuf/emailservice:latest ."
                        sh "docker push tkibnyusuf/emailservice:latest"
                        sh "docker rmi tkibnyusuf/emailservice:latest"
                    }
                }
            }
        }
            }
            stage('frontend') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/frontend/") {
                        sh "docker build -t tkibnyusuf/frontend:latest ."
                        sh "docker push tkibnyusuf/frontend:latest"
                        sh "docker rmi tkibnyusuf/frontend:latest"
                    }
                }
            }
        }
            }
            stage('loadgenerator') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/loadgenerator/") {
                        sh "docker build -t tkibnyusuf/loadgenerator:latest ."
                        sh "docker push tkibnyusuf/loadgenerator:latest"
                        sh "docker rmi tkibnyusuf/loadgenerator:latest"
                    }
                }
            }
        }
            }
             stage('paymentservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/paymentservice/") {
                        sh "docker build -t tkibnyusuf/paymentservice:latest ."
                        sh "docker push tkibnyusuf/paymentservice:latest"
                        sh "docker rmi tkibnyusuf/paymentservice:latest"
                    }
                }
            }
        }
             }
             stage('productcatalogservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/productcatalogservice/") {
                        sh "docker build -t tkibnyusuf/productcatalogservice:latest ."
                        sh "docker push tkibnyusuf/productcatalogservice:latest"
                        sh "docker rmi tkibnyusuf/productcatalogservice:latest"
                    }
                }
            }
        }
             }
             stage('recommendationservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/recommendationservice/") {
                        sh "docker build -t tkibnyusuf/recommendationservice:latest ."
                        sh "docker push tkibnyusuf/recommendationservice:latest"
                        sh "docker rmi tkibnyusuf/recommendationservice:latest"
                    }
                }
            }
        }
             }
             stage('shippingservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/shippingservice/") {
                        sh "docker build -t tkibnyusuf/shippingservice:latest ."
                        sh "docker push tkibnyusuf/shippingservice:latest"
                        sh "docker rmi tkibnyusuf/shippingservice:latest"
                    }
                }
            }
        }
    }

              stage('EKS-Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'myAppp-eks-cluster', contextName: '', credentialsId: 'k8s', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://525234472B0F4B2855BDA5EA0292CCCD.gr7.us-east-1.eks.amazonaws.com') {
                    sh 'kubectl apply -f deployment-service.yaml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'

                }
                }
            }
        }
   }
