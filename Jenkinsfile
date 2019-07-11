pipeline {
    agent none
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
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
         agent {
                docker {
                    image 'python:2-alpine'
                }
           }
	 steps {
	  sshPublisher(
	   continueOnError: false, failOnError: true,
	   publishers: [
	    sshPublisherDesc(
	     configName: "ml",
	     verbose: true,
	     transfers: [
	      sshTransfer(
	       sourceFiles: "*",
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
