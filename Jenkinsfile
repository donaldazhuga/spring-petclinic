pipeline {
    agent any
    triggers {
        cron('H/3 * * * 1') // Trigger every 3 minutes on Mondays
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Starting Build Stage'
                sh './mvnw clean package'
                echo 'Build Stage Completed'
            }
        }
        stage('Code Coverage Report') {
            steps {
                echo 'Running Code Coverage Report'
                sh './mvnw jacoco:report'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            jacoco execPattern: '**/target/*.exec', classPattern: '**/classes', sourcePattern: '**/src/main/java'
        }
    }
}
