library identifier: 'pipelineslib@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'file:///Users/shantur/Devops/Pipelines/retry-lib'])


pipeline {

    agent any

    environment {
        LOG_LEVEL = "5"
    }

    stages {

        stage('Stage1') {
            when {
                expression { return needToRunStage() }
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
                expression { return needToRunStage() }
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
                always {
                    echo 'Post always'
                }
            }
        }

    }

    post {
        always {
            archiveRetryData()
        }
    }
}


