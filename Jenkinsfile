pipeline {
    agent any

    tools {
        maven 'Default'
        jdk 'Default'
    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build & Test - Chrome') {
            steps {
                sh "mvn clean test -Dbrowser=chrome"
            }
        }

        stage('Build & Test - Firefox') {
            steps {
                sh "mvn clean test -Dbrowser=firefox"
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            emailext(
                subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: "Build was successful!\nCheck console output at ${env.BUILD_URL} to view the results.",
                to: 'your-email@example.com'
            )
        }
        failure {
            emailext(
                subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: "Build failed!\nCheck console output at ${env.BUILD_URL} to view the results.",
                to: 'your-email@example.com'
            )
        }
    }
}
