pipeline {
    agent any
    triggers {
        cron('H/3 * * * 1') // Trigger every 3 minutes on Mondays
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the source code'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Starting Build Stage'
                bat 'mvnw.cmd clean package' // Use mvnw.cmd for Windows
                echo 'Build Stage Completed'
            }
        }
        stage('Code Coverage Report') {
            steps {
                echo 'Running Code Coverage Report'
                bat 'mvnw.cmd test jacoco:report' // Use mvnw.cmd for Windows
                echo 'Code Coverage Report Generated'
            }
        }
    }
    post {
        always {
            echo 'Archiving artifacts and generating reports'
            archiveArtifacts artifacts: '/target/*.jar', fingerprint: true
            jacoco execPattern: '/target/jacoco.exec', classPattern: '/classes', sourcePattern: '/src/main/java'
        }
    }
}
