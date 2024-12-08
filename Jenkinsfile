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
                //    bat 'minikube delete'
                    bat 'minikube start'
                    
                    // Enable the dashboard addon
                    bat 'minikube addons enable dashboard'
                    
                    // Apply Kubernetes resources
                    bat 'kubectl apply -f deployment.yaml'
                 //   bat 'kubectl apply -f my-kube1-service.yaml'
                    
                    // Expose the Kubernetes Dashboard service
                    bat 'minikube dashboard'
                }
            }
        }
    }
}
