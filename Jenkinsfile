pipeline {
  agent {
    docker {
      image 'docker/compose:1.18.0'
    }
    
  }
  stages {
    stage('build') {
      steps {
        sh '''docker-compose build
docker-compose run install
'''
      }
    }
  }
}