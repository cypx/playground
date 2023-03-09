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
    tools {
        nodejs 'nodejs18'
    }
    stages {
        stage('nodejs') {
            steps {
                sh '''
                    cd nodejs
                    yarn install
                    yarn build
                '''
            }
        }
    }
}