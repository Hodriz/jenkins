pipeline {
    agent any
    
    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Hodriz/jenkins.git', branch: 'dev'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'ng test --watch=false --browsers=ChromeHeadless'
            }
        }
        
        stage('Build') {
            steps {
                sh 'ng build --prod'
            }
        }
    }
    
    post {
        always {
            junit 'coverage/**/*.xml'
            archiveArtifacts artifacts: 'dist/**/*.*', fingerprint: true
        }
    }
}
