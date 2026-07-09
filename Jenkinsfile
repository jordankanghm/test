pipeline {
    agent any

    tools {
        maven 'Maven3' // name must match what you configured in Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/<your-username>/hello-world-webapp.git'
                    // add credentialsId: 'github-creds' here if repo is private
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat10(credentialsId: 'tomcat-creds',
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