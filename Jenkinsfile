pipeline {
  agent any

  environment {
    TARGET = "/var/www/my-app"   // <-- tumhara actual target
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Deploy to Apache') {
      steps {
        sh '''
          set -e
          echo "Deploying to $TARGET"
          mkdir -p "$TARGET"
          rsync -av --delete --exclude='.git' ./ "$TARGET/"
          # reload apache (jenkins user must have sudo NOPASSWD for this)
          sudo systemctl reload apache2
        '''
      }
    }
  }
}
