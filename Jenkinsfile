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
                sh "echo Stage1 Build:${env.BUILD_NUMBER} > stage1.txt"
            }
            post {
                success {
                    archiveStageArtifacts('stage1.txt')
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
                 sh "echo Stage2 Build:${env.BUILD_NUMBER} > stage2.txt"
            }
            post {
                success {
                    archiveStageArtifacts('stage2.txt')
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


