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
        stage('java') {
            steps {
                sh '''
                    cd java
                    ./gradlew build -x test
                '''
            }
        }
        stage('php init') {
            agent {
                dockerfile {
                    filename             'Dockerfile'
                    dir                  'docker/php'
                    label                ''
                    additionalBuildArgs  ''
                    args                 ''
                }   
            }
            steps {
                sh 'cd php && composer install --no-interaction'
            }
        }
        stage('php test') {
            agent {
                dockerfile {
                    filename             'Dockerfile'
                    dir                  'docker/php'
                    label                ''
                    additionalBuildArgs  ''
                    args                 ''
                }
            }
            warnError('PHP tests failed!') {
                steps {
                    sh 'cd php && phpcs -p app/'
                }
            }
        }
    }
}