pipeline {
    agent any


    stages {

          stage('Cloning from Git') {
              steps {
                  checkout scm: [$class: 'GitSCM', userRemoteConfigs: [[url: "https://github.com/Netflix/conductor.git" ]]], poll: false
              }
          }

          stage('Building image') {
              steps {
                  sh 'docker build -t conductor:server -f docker/server/Dockerfile .'
              }
          }


          stage('push') {
              steps {
                   sh "echo 'Ankit@123docker' | docker login -u ankit@fynarfin.io --password-stdin"
                   sh 'docker push anover/conductor:server'
              }
          }
    }
}