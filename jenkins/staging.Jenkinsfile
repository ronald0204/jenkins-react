pipeline {
    agent {
        docker {
            image 'devillex/docker-firebase'
            args '-p 3001:3001'
        }
    }
    environment { 
        CI = 'true'
        FIREBASE_DEPLOY_TOKEN = credentials('firebase-deploy-token') 
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Staging') { 
            steps {
                sh './jenkins/scripts/staging.sh' 
                input message: 'Finished using the Staging version of the Web App? (Click "Proceed" to continue)' 
            }
        }
        stage('Production') { 
            steps {
                sh './jenkins/scripts/production.sh' 
            }
        }
    }
}