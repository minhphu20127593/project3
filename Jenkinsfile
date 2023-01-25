pipeline {
  agent any
  stages {
    stage('Clone Stage') {
      steps {
        git credentialsId: 'Git', url: 'https://github.com/minhphu20127593/project3.git'
      }
    }
    stage('Docker Build'){
      steps{
        sh 'docker build -t 20127593/project3:latest .'
      }
    }
    stage('Docker Push'){
      steps{
        withDockerRegistry(credentialsId: 'docker-hub', url: 'https://index.docker.io/v1/') {
        sh 'docker push 20127593/project3:latest .'
        }
      }
    }
    stage('Docker Deploy') {
      steps {
        sh 'docker start jenkins || docker run -d --name jenkins --publish 8080:8080 20127593/project3:latest'
      }
    }
    stage('Docker Testing') {
      steps {
        sh 'docker exec --tty jenkins curl https://localhost:8080/testing'
      }
    }
  }
}
