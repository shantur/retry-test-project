library identifier: 'pipelineslib@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'file:///Users/shantur/Devops/Pipelines/retry-lib'])


def previousRetryData = loadRetryData()

pipeline {

    agent any

//    environment {
//        RETRY_DATA = loadRetryData()
//    }

    stages {

//        stage('Initialize') {
//            steps {
//                loadRetryData()
//            }
//        }

        stage('Stage1') {
            when {
                expression { return needToRunStage(previousRetryData) }
            }
            steps {
                echo 'Running Stage 1'
            }
        }

        stage('Stage2') {
            when {
                expression { return needToRunStage(previousRetryData) }
            }
            steps {
                echo 'Running Stage 2'
            }
        }

    }

//    post {
//        always {
////            saveRetryData()
//        }
//    }
}


