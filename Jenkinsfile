pipeline {
  agent {
    node {
      label 'facjenkinsl408'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t dockersamples/result ./result'
      }
    }
    stage('Build vote') {
      steps {
        sh 'docker build -t dockersamples/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t dockersamples/worker ./worker'
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: '12345678900987654321', url:'') {
          sh 'docker push dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: '12345678900987654321', url:'') {
          sh 'docker push dockersamples/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: '12345678900987654321', url:'') {
          sh 'docker push dockersamples/worker'
        }
      }
    }
  }
}