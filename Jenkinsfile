pipeline {
  agent any

  environment {
    TARGET = "/var/www/my-app"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Debug') {
      steps {
        sh '''
          echo "==== DEBUG INFO ===="
          echo "Current directory: $(pwd)"
          echo "Files in current dir:"
          ls -l
          echo "===================="
        '''
      }
    }

    stage('Deploy to Apache') {
      steps {
        sh '''
          set -e
          echo "Deploying to $TARGET"
         
          rsync -av --delete --exclude='.git' ./ "$TARGET/"
          
        '''
      }
    }
  }
}

