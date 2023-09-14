pipeline {
    agent any

    stages {
        stage('Build and Push') {
            steps {
                script {
                    // Checkout code
                    checkout scm

                    // Start Docker
                    sh 'docker info'

                    // Clone Git repository
                    if (fileExists('conductor')) {
                        // If it exists, update the repository
                        dir('conductor') {
                            sh 'git pull origin master'
                        }
                    } else {
                        // If not, clone the repository
                        sh 'git clone https://github.com/Netflix/conductor.git'
                    }

                    // Build Conductor Server Docker Image
                    dir('conductor/docker') {
                        sh 'docker-compose -f docker-compose.yaml -f docker-compose-postgres.yaml build'
                    }

                    // Push Conductor Server Docker Image
                    sh "echo 'Ankit@123docker' | docker login -u ankit@fynarfin.io --password-stdin"
                    sh 'docker push anover/conductor:server'

                    // Push Conductor UI Docker Image
                    sh "echo 'Ankit@123docker' | docker login -u ankit@fynarfin.io --password-stdin"
                    sh 'docker push anover/conductor:ui'
                }
            }
        }
    }
}