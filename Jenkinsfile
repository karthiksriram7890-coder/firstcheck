pipeline {
  agent any
  tools { nodejs 'NodeJS-20' }

  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Install') {
      steps {
        bat 'npm ci'
        bat 'npx playwright install'
      }
    }
    stage('Test') { steps { bat 'npx playwright test' } }
  }

  post {
    always {
      publishHTML(target: [
        reportDir: 'playwright-report',
        reportFiles: 'index.html',
        reportName: 'Playwright Report',
        keepAll: true,
        allowMissing: true
      ])
    }
  }
}