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
        stage('Deliver') { 
          sshPublisher {
            server('myhostname1.com') {
                credentials('remoteuser') {
                key: '''-----BEGIN RSA PRIVATE KEY-----
                MIIEowIBAAKCAQEAznShdsv0Z6pT9nSeyHdQqSP427/72dkrmxG7BPr9pDvBBOnb
                Y2agvw5/iuH+FsIjEoisBXh+DLN/H+7G9FuQO49Z5u16JRy3b8BOPF5qiGKagxw3
                YlPLFslT6vAOQ36H77+u4Scn4JTSKVext93PimXu3wY5amfgZy0ygAEtP/JbOJz3
                Fzl14wMoIGlxwYUDo6mq6Wk2l/xxQmH94y1MczosTjzjgC0r720o
                -----END RSA PRIVATE KEY-----'''
                }
                label('myhostname')
                transferSet {
                sourceFiles("**/*.zip")
                remoteDirectory('builds/\'yyyy/MM/dd/\'build-${BUILD_NUMBER}')
                execCommand('mkdir deployfolder & unzip myproject-${version}.zip')
                }
            }
          }
       }
    }
}
