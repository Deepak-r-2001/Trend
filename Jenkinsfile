pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "deepwhoo/trend-app"
        AWS_REGION = "ap-south-1"                                // 🔧 Region of your EKS cluster
        CLUSTER_NAME = "brain-tasks-cluster"                     // 🔧 Name of your EKS cluster
    }

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Deepak-r-2001/Trend.git', branch: 'main'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

        stage('Deploy to EKS') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-creds'                // 🔧 Add AWS credentials to Jenkins with this ID
                ]]) {
                    sh '''
                        aws eks --region $AWS_REGION update-kubeconfig --name $CLUSTER_NAME
                        kubectl apply -f deployment.yaml
                        kubectl apply -f service.yaml
                    '''
                }
            }
        }
    }
}

