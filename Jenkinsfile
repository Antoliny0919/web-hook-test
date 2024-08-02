import groovy.json.JsonSlurper

def repositoryName = null
def pullRequestState = null
def IMAGE_TAG = null

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
          input {
            message "Please enter the image version to be created. format v{major}.{minor}.{patch}"
            ok "Submit"
            parameters {
              string(name: "TAG", defaultValue: "latest", description: "Tag of the image to be distributed")
            }
          }
          steps {
	    script {
              IMAGE_TAG = sh(returnStdout: true, script: "echo $TAG").trim()
            }
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
