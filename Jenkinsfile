pipeline {
    agent any

    tools {
        maven 'Default'
        jdk 'Default'
    }

    triggers {
        pollSCM('H/5 * * * *') // Checks repo every 5 minutes
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
                subject: "✅ Build Successful - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build was successful!\n\nCheck details: ${env.BUILD_URL}",
                to: 'your-email@example.com'
            )
        }
        failure {
            emailext(
                subject: "❌ Build Failed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build failed!\n\nCheck details: ${env.BUILD_URL}",
                to: 'your-email@example.com'
            )
        }
    }
}

////////////