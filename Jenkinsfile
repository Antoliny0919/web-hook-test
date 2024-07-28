pipeline {
  agent any
  
  parameters { string(name: 'IMAGE_TAG', defaultValue: '', description: 'docker image tag') }

//   environment {
//     IMAGE_TAG = "$WEB_DEPLOY_IMAGE_TAG"
//   }

  stages {
    stage('Build') {
      steps {
	    sh '''
        echo "Build Step!!"
        echo "$IAMGE_TAG"
	    '''
      }
    }
    stage('Deploy') {
      steps {
        sh '''
        echo "Deploy Step!!"
        '''
      }
    }
    stage('Build Prod') {
      steps {
        sh '''
        echo "Build Prod env stage"
        '''
      }
    }
  }
}
