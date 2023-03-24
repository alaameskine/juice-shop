pipeline {
    agent any
    tools {
        nodejs "NodeJS"
    }
     stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'npm install sonarqube-scanner --save-dev'
                    sh './node_modules/.bin/sonar-scanner'  
                }
            }
        }
        
    stages {
        stage('Build') {
            steps {
                sh 'npm install'   
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