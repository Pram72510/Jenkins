pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    environment {
        APP_NAME = 'springboot-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/springboot-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            when {
                expression { fileExists('Dockerfile') }
            }
            steps {
                sh "docker build -t $APP_NAME:latest ."
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo '💡 Add deployment steps here'
            }
        }
    }

    post {
        success {
            echo '✅ Build succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}