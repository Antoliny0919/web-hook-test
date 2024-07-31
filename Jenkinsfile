import groovy.json.JsonSlurper

def repositoryName = null
def pullRequestState = null

pipeline {
  agent any
  
  parameters { string(name: 'payload', defaultValue: '', description: 'test') }

  environment {
    TAG = sh(returnStdout: true, script: "git tag --points-at=HEAD")
  }

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
          input {
            message "Please enter the image version to be created."
            ok "format v{major}.{minor}.{patch}"
            parameters {
              string(name: "IMAGE_TAG", defaultValue: "latest", description: "Tag of the image to be distributed")
            }
          }
          steps {
	    echo "$IMAGE_TAG print now tag!!"
          }
        }
        stage("Deploy") {
          steps {
            echo "deploy process $IMAGE_TAG"
          }
        }
      }
    }
  }
} 
