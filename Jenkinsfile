pipeline {
    agent none 
        stage('deploy') {
             steps {
              sshPublisher(
               continueOnError: false, failOnError: true,
               publishers: [
                sshPublisherDesc(
                 configName: "${env.SSH_CONFIG_NAME}",
                 verbose: true,
                 transfers: [
                  sshTransfer(
                   sourceFiles: "/var/jenkins_home/workspace/simple-python-pyinstaller-app/**/*",
                   removePrefix: "",
                   remoteDirectory: "python-test",
                   execCommand: "run commands after copy?"
                  )
                 ])
               ])
             }
        }
    }
