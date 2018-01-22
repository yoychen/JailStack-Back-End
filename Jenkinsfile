pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        dockerfile {
          filename 'docker/php7.2-cli/Dockerfile'
        }
        
      }
      steps {
        sh '''composer install
cp docker/php7.2-cli/.env.development.example .env
php artisan key:generate
php artisan vendor:publish --provider="Tymon\\JWTAuth\\Providers\\LaravelServiceProvider"
php artisan jwt:secret -f
ls -al'''
        stash 'tutu'
      }
    }
    stage('test') {
      agent {
        docker {
          image 'php'
        }
        
      }
      steps {
        unstash 'tutu'
        sh '''ls -al
./vendor/bin/phpunit'''
      }
    }
  }
}