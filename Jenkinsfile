pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'TP03', url: 'https://github.com/tra99/DevOp.git'
            }
        }
        stage('Composer') {
            steps {
                sh 'composer install'
            }
        }
        stage('Copy .env'){
            steps{
                sh 'cp .env.example .env'
            }
        }
        stage('AppKey'){
            steps{
                sh 'php artisan key:generate'
            }
        }
        stage('npm'){
            steps{
                sh 'npm i'
                sh 'npm run build'
            }
        }
        stage('test'){
            steps{
                sh 'php artisan test'
            }
        }
    }
    post {
        success {
            echo 'Build succeeded! Deploying...'
            // Add deployment trigger here
        }
        failure {
            mail to: 'chetrafc60@email.com',
                 subject: "Build Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                 body: "The build of ${env.JOB_NAME} ${env.BUILD_NUMBER} failed. Please check the Jenkins console output for more information."
        }
    }
}
