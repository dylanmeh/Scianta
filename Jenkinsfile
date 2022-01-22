pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: build
    image: 'maven:3.8.3-jdk-11'
    command:
    - cat
    tty: true
    '''
        defaultContainer 'build'
        }
    }
    stages {
        stage('build') {
            steps {
                sh 'echo "npm release"'
            }       
        }
    
        stage('test') {
            steps {
                sh 'echo "npm test"'
            }
        }

        stage('deploy') {
            steps {
                sh 'echo "deployment script"'
            }
        }
    }

    post {
        failure {
            emailext (
                subject: "Failure: Job '${env.JOB_NAME} [${env.BUOLD_NUMBER}]'",
                body: """Failure: Job '${JOB_NAME}' [${BUILD_NUMBER}]':
                Check console output at ${BUILD_URL}""",
                to: 'ted.fenn@concanon.com'
            )
        }
    }
} 