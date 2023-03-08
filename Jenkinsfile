pipeline {
    agent {
        label {
        label ""
        customWorkspace "workspace/"+"playground-${BRANCH_NAME}-${BUILD_ID}".replaceAll("/","-")
        }
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '20'))
    }
    stages {
        stage('test') {
            steps {
                sh '''
                    echo "hello world"
                '''
            }
        }
    }
}