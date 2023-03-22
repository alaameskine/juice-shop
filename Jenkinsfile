pipeline {
    agent any
    tools {
        nodejs "node"
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'   
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test'    
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'npm install sonarqube-scanner --save-dev'
                    sh './node_modules/.bin/sonar-scanner'  
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            junit 'target/surefire-reports/**/*.xml'
        }
    }
}
 //?