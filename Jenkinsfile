pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: "https://github.com/Modia12/siteVitrine.git"
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                }
                dir('backend') {
                    sh 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                sh "docker build -t sitevitrine-frontend -f Dockerfile.frontend ."
                sh "docker build -t sitevitrine-backend -f Dockerfile.backend ."
            }
        }

        stage('Deploy') {
            steps {
                sh "docker-compose down"
                sh "docker-compose up -d --build"
            }
        }
    }
}
