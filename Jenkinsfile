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
            agent {
                docker {
                    image 'qnib/pytest'
                }
            }
            steps {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
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
