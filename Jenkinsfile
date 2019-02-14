library identifier: 'pipelineslib@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'file:///Users/shantur/Devops/Pipelines/retry-lib'])


//def previousRetryData = loadRetryData()

pipeline {

    agent any

    environment {
        PREVIOUS_RETRY_DATA = loadRetryData()
        CURRENT_RETRY_DATA = "{ }"
    }

    stages {

//        stage('Initialize') {
//            steps {
//                loadRetryData()
//            }
//        }

        stage('Stage1') {
            when {
                expression { return needToRunStage(PREVIOUS_RETRY_DATA) }
            }
            steps {
                echo 'Running Stage 1'
            }
            post {
                success {
                    setStageResult(true)
                }
                unsuccessful {
                    setStageResult(false)
                }
            }
        }

        stage('Stage2') {
            when {
                expression { return needToRunStage(PREVIOUS_RETRY_DATA) }
            }
             steps {
                echo 'Running Stage 2'
            }
            post {
                success {
                    setStageResult(true)
                }
                unsuccessful {
                    setStageResult(false)
                }
            }
        }

    }

//    post {
//        always {
////            saveRetryData()
//        }
//    }
}


