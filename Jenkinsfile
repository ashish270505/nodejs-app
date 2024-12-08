pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("ashish2705/nodejs-app:${env.BUILD_NUMBER}", ".")
                }
            }
        }
        
        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'd125f44d-440b-4b8d-9d9e-217ea52911e0') {
                        dockerImage.push()
                    }
                }
            }
        }
         stage('Deploy to Kubernetes') {
            steps {
                script {
                    withCredentials([file(credentialsId:k8s-cluster-credentials,variable:CONFIG)])
                  {  // Apply deployment and service YAML files
                    bat 'kubectl apply -f Deployment.yaml'
                    //bat 'kubectl apply -f service.yaml'
                    bat 'kubectl get deployments'}
                }
            }
        }
    }
}