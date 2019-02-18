library identifier: 'pipelineslib@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'file:///Users/shantur/Devops/Pipelines/retry-lib'])


pipeline {

    agent any

    environment {
        LOG_LEVEL = "5"
    }

    parameters {
        booleanParam(name: 'FORCE_REBUILD', defaultValue: false, description: 'Force Rebuild')
        booleanParam(name: 'STAGE_1_SUCCESS', defaultValue: true, description: 'Make Stage 1 pass')
        booleanParam(name: 'STAGE_2_SUCCESS', defaultValue: true, description: 'Make Stage 2 pass')
        booleanParam(name: 'TEST_STAGE_1_SUCCESS', defaultValue: true, description: 'Make Test Stage 1 pass')
        booleanParam(name: 'TEST_STAGE_2_SUCCESS', defaultValue: true, description: 'Make Test Stage 2 pass')

    }

    stages {
        stage('Build') {
            failFast false
            parallel {
                stage('Stage1') {
                    when {
                        expression { return needToRunStage() }
                    }
                    steps {
                        echo 'Running Stage 1'
                        sh "echo Stage1 Build:${env.BUILD_NUMBER} > stage1.txt"
                        failStageIfNeeded(params.STAGE_1_SUCCESS)
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
                        echo 'Running Stage 2 with feature2'
                        sh "echo Stage2 feature 2   Build:${env.BUILD_NUMBER} > stage2.txt"
                        failStageIfNeeded(params.STAGE_2_SUCCESS)
                    }
                    post {
                        success {
                            archiveStageArtifacts('stage2.txt')
                            setStageResult(true)
                        }
                        unsuccessful {
                            setStageResult(false)
                        }
                    }
                }
            }
        }


        stage('Test') {
            failFast false
            parallel {
                stage('Test Stage1') {
                    when {
                        expression { return needToRunStage() }
                    }
                    steps {
                        echo 'Running Test Stage 1'
                        sh "echo test Stage1 Build:${env.BUILD_NUMBER} > teststage1.txt"
                        failStageIfNeeded(params.TEST_STAGE_1_SUCCESS)
                    }
                    post {
                        success {
                            archiveStageArtifacts('teststage1.txt')
                            setStageResult(true)
                        }
                        unsuccessful {
                            setStageResult(false)
                        }
                    }
                }

                stage('Test Stage2') {
                    when {
                        expression { return needToRunStage() }
                    }
                    steps {
                        echo 'Running test Stage 2'
                        sh "echo test Stage2 Build:${env.BUILD_NUMBER} > teststage2.txt"
                        failStageIfNeeded(params.TEST_STAGE_2_SUCCESS)
                    }
                    post {
                        success {
                            archiveStageArtifacts('teststage2.txt')
                            setStageResult(true)
                        }
                        unsuccessful {
                            setStageResult(false)
                        }
                    }
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

def failStageIfNeeded(boolean success) {
    if (!success) {
        sh 'exit 1'
    }
}


