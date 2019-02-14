library identifier: 'pipelineslib@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'file:///Users/shantur/Devops/Pipelines/retry-lib'])


pipeline {

    agent any

//    environment {
//        RETRY_DATA = loadRetryData()
//    }

    stages {

        stage('Initialize') {
            steps {
                loadRetryData()
            }
        }

        stage('Stage1') {
            steps {
                runStageIfNeeded() {
                    echo 'Running Stage 1'
                }
            }
        }

        stage('Stage2') {
            steps {
                runStageIfNeeded() {
                    echo 'Running Stage 2'
                }
            }
        }

    }

    post {
        always {
            saveRetryData()
        }
    }
}


