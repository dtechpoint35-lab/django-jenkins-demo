pipeline {
    agent any

    stages {

        stage('Code') {
            steps {
                echo "Cloning Code..."
                git 'https://github.com/YOUR-USERNAME/django-jenkins-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building Docker Image..."
                sh 'sudo docker build -t django-app .'
            }
        }

        stage('Test') {
            steps {
                echo "Checking Docker Image..."
                sh 'sudo docker images'
            }
        }

        stage('Deploy') {
            steps {
                echo "Running Container..."
                sh '''
                sudo docker stop django-container || true
                sudo docker rm django-container || true
                sudo docker run -d -p 8000:8000 --name django-container django-app
                '''
            }
        }
    }

    post {
        success {
            echo "🎉 CI/CD SUCCESS"
        }
        failure {
            echo "❌ FAILED"
        }
    }
}
