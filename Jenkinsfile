pipeline {
    agent any

    tools {
        jdk 'JDK17'
    }

    triggers {
        cron('H/5 * * * 1')
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvnw.cmd clean package'
            }
        }

        stage('JaCoCo Coverage') {
            steps {
                bat 'mvnw.cmd jacoco:report'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            junit 'target/surefire-reports/*.xml'
        }
    }
}