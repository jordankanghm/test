pipeline {
    agent any

    tools {
        maven 'maven' // name must match what you configured in Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/jordankanghm/test.git'
                    // add credentialsId: 'github-creds' here if repo is private
            }
        }

        stage('Build') {
            steps {
                bat 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-creds',
                                          url: 'http://localhost:9090/')],
                       contextPath: 'helloapp',
                       war: '**/target/helloapp.war'
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded! ✅'
        }
        failure {
            echo 'Deployment failed! ❌'
        }
    }
}