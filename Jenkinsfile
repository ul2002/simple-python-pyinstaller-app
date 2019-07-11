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
                
            }
        }
        stage('Test') {
            steps {
             
            }
            post {
                always {
                    junit 'test-reports/results.xml'
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
