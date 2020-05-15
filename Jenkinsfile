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
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push 12345678900987654321/dockersamples/result:latest'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push 12345678900987654321/dockersamples/vote:latest'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push 12345678900987654321/dockersamples/worker:latest'
        }
      }
    }
  }
}