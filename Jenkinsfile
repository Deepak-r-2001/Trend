pipeline {
    agent any

    environment {
        IMAGE_NAME = 'your-dockerhub-username/trend'
        CLUSTER_NAME = 'brain-tasks-cluster'
        REGION = 'ap-south-1'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Vennilavan12/Trend.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    sh '''
                      echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                      docker push $IMAGE_NAME
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-eks-creds']]) {
                    sh '''
                      aws eks update-kubeconfig --region $REGION --name $CLUSTER_NAME
                      kubectl apply -f deployment.yaml
                      kubectl apply -f service.yaml
                    '''
                }
            }
        }
    }
}
