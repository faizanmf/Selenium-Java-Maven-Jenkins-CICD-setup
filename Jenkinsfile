pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/selenium-ci-cd.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Report') {
            steps {
                publishHTML([allowMissing: false,
                             alwaysLinkToLastBuild: false,
                             keepAll: true,
                             reportDir: 'target/surefire-reports',
                             reportFiles: 'index.html',
                             reportName: 'TestNG Report'])
            }
        }
    }
}
