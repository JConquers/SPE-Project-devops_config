pipeline {
  agent any

  stages {

    stage('Checkout Config Repo') {
      steps {
        checkout scm
      }
    }

    stage('Apply Kubernetes Manifests') {
      steps {
        sh """
          kubectl apply -f namespaces/
          kubectl apply -f backend/
          kubectl apply -f frontend/
          kubectl apply -f ingress/
        """
      }
    }
  }

  post {
    success {
      echo "Kubernetes manifests applied successfully."
    }
    failure {
      echo "Failed applying Kubernetes manifests."
    }
  }
}
