import groovy.json.JsonSlurper

def repositoryName = null
def pullRequestState = null

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
	      def myobj = new JsonSlurper().parseText(payload)
	      repositoryName = myobj.repository.full_name
	      pullRequestState = myobj.pull_request.state
	      if(pullRequestState == "open") {
		  echo "it is open state"
		  sh "exit 1"
		}
	      
	    }
	}
    } 
    stage('Build') {
      steps {
	sh "echo ${repositoryName} it is build step and use variable"	   
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
