pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("ashish2705/nodejs-app:latest", ".")
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
