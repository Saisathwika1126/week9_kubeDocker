pipeline {
    agent any
    stages
    {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                sh "docker build -t kubdemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  sh 'docker login -u saisathwika1126 -p Sathwika@1126'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                sh "docker tag kubdemoapp:v1 saisathwika1126/docker_week8:kubeimage1"               
                    
                sh "docker push saisathwika1126/docker_week8:kubeimage1"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    // apply deployment & service 
                    sh 'kubectl apply -f deployment.yaml --validate=false' 
                    sh 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}