pipeline {
    agent any
    triggers {
        cron('H/3 * * * 1') 
    }
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        stage('Code Coverage Report') {
            steps {
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
