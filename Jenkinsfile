pipeline {
    agent any
    stages
    {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t mypythonflaskapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u swathi1276 -p Docker@123'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag mypythonflaskapp:v1 swathi1276/week8:latest"               
                    
                bat "docker push swathi1276/week8:latest"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    // apply deployment & service 
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
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
