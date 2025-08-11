pipeline {
  agent any
  tools { maven 'Maven 3.9' } // name from Global Tool Configuration
  stages {
    stage('Checkout') {
      steps { checkout scm }
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
  triggers {
    // cron example (optional)
    // cron('H H * * *')
  }
}
