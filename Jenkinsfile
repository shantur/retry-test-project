library identifier: 'pipelineslib@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'file:///Users/shantur/Devops/Pipelines/retry-lib'])


pipeline {

    agent any

    environment {
        loadRetryData()
    }

    stages {

        stage('Stage1') {
            runStageIfNeeded() {
                echo 'Running Stage 1'
            }
        }

        stage('Stage2') {
            runStageIfNeeded() {
                echo 'Running Stage 2'
            }
        }

    }

    post {
        always {
            saveRetryData()
        }
    }
}


