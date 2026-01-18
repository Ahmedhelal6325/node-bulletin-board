pipeline {
  agent any

  environment {
    APP_NAME = "bulletin-board"
    APP_PORT = "9090"
  }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/Ahmedhelal6325/node-bulletin-board.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh '''
        docker build -t $APP_NAME:$BUILD_NUMBER .
        '''
      }
    }

    stage('Run Container') {
      steps {
        sh '''
        docker rm -f $APP_NAME || true
        docker run -d \
          --name $APP_NAME \
          -p $APP_PORT:$APP_PORT \
          $APP_NAME:$BUILD_NUMBER
        '''
      }
    }
  }
}
