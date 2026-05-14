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
                script {
                    docker.build("soc-app")
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh 'docker rm -f soc-container || true'
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name soc-container soc-app'
                }
            }
        }
    }
}