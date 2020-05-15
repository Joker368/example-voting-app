pipeline {
  agent {
    node {
      label 'facjenkinsl408'
    }
  }
  stages {
    stage('Clean') {
      steps {
        sh 'docker image prune -f'
      }
    }
    stage('Build result') {
      steps {
        sh 'docker build -t docker.io/12345678900987654321/dockersamples_result ./result'
      }
    }
    stage('Build vote') {
      steps {
        sh 'docker build -t docker.io/12345678900987654321/dockersamples_vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t docker.io/12345678900987654321/dockersamples_worker ./worker'
      }
    }
    stage('Push result image') {
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push docker.io/12345678900987654321/dockersamples_result:latest'
        }
      }
    }
    stage('Push vote image') {
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push docker.io/12345678900987654321/dockersamples_vote:latest'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: 'jm026829.docker-registry', url:'') {
          sh 'docker push docker.io/12345678900987654321/dockersamples_worker:latest'
        }
      }
    }
  }
  post {
    always {
      script {
        sh 'docker container prune -f' /* remove stopped containers */
        sh 'docker image rmi $(docker images --format="{{.Repository}} {{.ID}}" |  grep "12345678900987654321_*" |  cut -d' ' -f2) -f'
      }
    }
  }
}