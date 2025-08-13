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
                    url: 'https://github.com/faizanmf/Selenium-Java-Maven-Jenkins-CICD-setup.git'
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

            emailext(
                to: 'faizanmf.5252@gmail.com',
                subject: "Jenkins Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """<p>Hi,</p>
                         <p>The Jenkins build has completed with status: <b>${currentBuild.currentResult}</b></p>
                         <p>Check console output at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                mimeType: 'text/html'
            )
        }
    }
}
