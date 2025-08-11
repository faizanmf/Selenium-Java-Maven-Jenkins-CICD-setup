pipeline {
    agent any

    tools {
        maven 'Maven 3.9' // Name as configured in "Manage Jenkins" → Global Tool Configuration
    }

    triggers {
        cron('H H * * *') // Run every 5 minutes
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                sh 'mvn -B clean test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                    archiveArtifacts artifacts: '**/target/*.jar, **/target/allure-results/**', fingerprint: true
                }
            }
        }
    }
}
