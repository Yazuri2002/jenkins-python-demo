pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo 'Código listo'
      }
    }
    stage('Setup Python') {
      steps {
        bat 'python -m venv venv'
        bat 'venv\\Scripts\\pip install --upgrade pip'
        bat 'venv\\Scripts\\pip install -r requirements.txt'
      }
    }
    stage('Test') {
      steps {
        bat 'venv\\Scripts\\pytest -q --junitxml=reports\\junit.xml'
      }
    }
    stage('Publicar Reporte') {
      steps {
        junit allowEmptyResults: false, testResults: 'reports/junit.xml'
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: 'reports/junit.xml', onlyIfSuccessful: false
    }
  }
}
