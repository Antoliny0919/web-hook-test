pipeline {
  agent any
  
  parameters { string(name: 'payload', defaultValue: '', description: 'test') }

//   environment {
//     IMAGE_TAG = "$WEB_DEPLOY_IMAGE_TAG"
//   }

  stages {
    stage('get git branch name') {
	steps {
	  script {
	      def myobj = readJSON text: payload
	      echo "repository full name is ${myobj.repository.full_name}"
	    }
	}
    } 
    stage('Build') {
      steps {
	    sh '''
        echo "Build Step!!"
        echo "$payload"
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
