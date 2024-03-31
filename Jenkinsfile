pipeline {
    agent any
    stages {
        stage('Build the docker image and push to registry.') {
            steps {
                sh 'docker build . -t 172.23.8.1:9500/labelprinter:latest --no-cache'
                sh 'docker image push 172.23.8.1:9500/labelprinter:latest'
            }
        }

        stage('Deploy to the minikube') {
            steps {
                dir('deployment') {
                    sh 'microk8s kubectl apply -f deployment.yaml'
                    sh 'microk8s kubectl apply -f labelPrinter-Svc.yaml'
                    sh 'microk8s kubectl rollout restart deployment labelprinter'
                }
            }
        }

    }
}
