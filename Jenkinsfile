import groovy.json.JsonSlurper

def repositoryName = null
def pullRequestState = null

pipeline {
  agent any
  
  parameters { string(name: 'payload', defaultValue: '', description: 'test') }

  stages {
    stage("parse-params") {
      steps {
        script {
	  def myobj = new JsonSlurper().parseText(payload)
	  repositoryName = myobj.repository.full_name
	  pullRequestState = myobj.pull_request.state
        }
      }
    }
    stage("opened") {
      when {
        expression { return pullRequestState == "open" }
      }
      stages {
        stage("Test") {
          steps {
            echo "A testing process is required. Pytest"
          }
        }
      }
    }
    stage("closed") {
      when {
        expression { return pullRequestState == "closed" }
      }
      stages {
        stage("Build") {
          steps {
            echo "build process"
          }
        }
        stage("Deploy") {
          steps {
            echo "deploy process"
          }
        }
      }
    }
  }
} 
