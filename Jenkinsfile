pipeline {
    agent {
        docker {
            image 'python:2-alpine'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                 sh ''
            }
        }
        stage('Test') {
            steps {
              sh ''
            }
            post {
                always {
                    junit ''
                }
            }
        }
        
	stage('SSH transfer') {
	 steps {
	  sshPublisher(
	   continueOnError: false, failOnError: true,
	   publishers: [
	    sshPublisherDesc(
	     configName: "ml",
	     verbose: true,
	     transfers: [
	      sshTransfer(
	       sourceFiles: "",
	       removePrefix: "",
	       remoteDirectory: "tmp",
	       execCommand: "ls"
	      )
	     ])
	   ])
	 }
	}
    }
}
