pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-node-app"
        DOCKER_HUB_USER = "anuragrajput26"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/AnuragRajput-cyber/Jenkins-Pipeline-for-CI-CD.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'echo Running tests...'
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t %DOCKER_HUB_USER%/%IMAGE_NAME% ."
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat """
                        docker login -u %USERNAME% -p %PASSWORD%
                        docker push %DOCKER_HUB_USER%/%IMAGE_NAME%
                    """
                }
            }
        }

        stage('Deploy (Optional)') {
            steps {
                bat 'echo Deployment logic goes here'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
