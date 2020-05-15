pipeline {
  agent {
    node {
      label 'facjenkinsl408'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t docker.io/12345678900987654321/dockersamples ./result'
      }
    }
    stage('Build vote') {
      steps {
        sh 'docker build -t docker.io/12345678900987654321/dockersamples ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t docker.io/12345678900987654321/dockersamples ./worker'
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push docker.io/12345678900987654321/dockersamples:latest'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push docker.io/12345678900987654321/dockersamples:latest'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push docker.io/12345678900987654321/dockersamples/worker:latest'
        }
      }
    }
  }
}