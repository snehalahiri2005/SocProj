pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/snehalahiri2005/SocProj.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t soc-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop soc-container || exit 0'
                bat 'docker rm soc-container || exit 0'
            }
        }

        stage('Run New Container') {
            steps {
                bat 'docker run -d -p 5000:5000 --name soc-container soc-app'
            }
        }
    }
}