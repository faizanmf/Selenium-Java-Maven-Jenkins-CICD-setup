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
    }
}
////////////