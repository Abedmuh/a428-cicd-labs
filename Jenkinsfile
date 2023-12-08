pipeline {
    triggers {
        pollSCM('H/2 * * * *') 
    }
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000' 
        }
    }
    
    
    stages {
        stage('Git prep') {
            steps {
                git branch: 'react-app', url: 'https://github.com/Abedmuh/a428-cicd-labs'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm cache clean --force'
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh'
                input message: 'Lanjutkan ke tahap Deploy?' 
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                sh 'sleep 60'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
