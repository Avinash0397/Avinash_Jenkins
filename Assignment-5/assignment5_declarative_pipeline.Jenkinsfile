pipeline {
    agent any

    environment {
        SLACK_CHANNEL = '#test'
        EMAIL_RECIPIENTS = 'avimishra478@gmail.com'
    }

    parameters {
        booleanParam(name: 'SKIP_STABILITY_CHECK', defaultValue: true, description: 'Skip Code Stability Check')
        booleanParam(name: 'SKIP_QUALITY_ANALYSIS', defaultValue: false, description: 'Skip Code Quality Analysis')
        booleanParam(name: 'SKIP_COVERAGE_ANALYSIS', defaultValue: false, description: 'Skip Code Coverage Analysis')
    }

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/builderHub/CICD-01.git'
            }
        }

        stage('Run Parallel Checks') {
            parallel {
                stage('Code Stability Check') {
                    when {
                        expression { return !params.SKIP_STABILITY_CHECK }
                    }
                    steps {
                        echo 'Running Unit Tests (JUnit)...'
                        sh 'mvn test'
                        junit '**/target/surefire-reports/*.xml'
                    }
                }

                stage('Code Quality Analysis') {
                    when {
                        expression { return !params.SKIP_QUALITY_ANALYSIS }
                    }
                    steps {
                        echo 'Running Checkstyle...'
                        sh 'mvn checkstyle:checkstyle'
                        archiveArtifacts artifacts: '**/target/site/checkstyle.html', allowEmptyArchive: true
                    }
                }

                stage('Code Coverage Analysis') {
                    when {
                        expression { return !params.SKIP_COVERAGE_ANALYSIS }
                    }
                    steps {
                        echo 'Running JaCoCo Coverage...'
                        sh 'mvn jacoco:report'
                        archiveArtifacts artifacts: '**/target/site/jacoco/index.html', allowEmptyArchive: true
                    }
                }
            }
        }

        stage('Generate Report') {
            steps {
                echo 'Reports archived. Please check Jenkins artifacts tab.'
            }
        }

        stage('Approval Before Publish') {
            steps {
                script {
                    def userInput = input(
                        id: 'Approval',
                        message: 'Do you want to proceed with publishing the artifacts?',
                        parameters: [
                            choice(name: 'Publish Artifacts', choices: ['Yes', 'No'], description: 'Approve to publish or deny')
                        ]
                    )

                    if (userInput == 'Yes') {
                        currentBuild.result = 'SUCCESS'
                    } else {
                        currentBuild.result = 'ABORTED'
                        error("Artifact publishing denied by user.")
                    }
                }
            }
        }

        stage('Publish Artifacts') {
            when {
                expression { return currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Publishing artifacts...'
                // Implement actual logic if using Nexus/S3 etc.
            }
        }
    }

    post {
        success {
            slackSend(channel: SLACK_CHANNEL, message: "Build SUCCESSFUL: ${env.JOB_NAME} #${env.BUILD_NUMBER}")
            emailext(to: EMAIL_RECIPIENTS, subject: "Build SUCCESS - ${env.JOB_NAME}", body: "Build ${env.BUILD_NUMBER} succeeded.")
        }

        failure {
            slackSend(channel: SLACK_CHANNEL, message: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}")
            emailext(to: EMAIL_RECIPIENTS, subject: "Build FAILED - ${env.JOB_NAME}", body: "Build ${env.BUILD_NUMBER} failed.")
        }

        aborted {
            slackSend(channel: SLACK_CHANNEL, message: "Build ABORTED: ${env.JOB_NAME} #${env.BUILD_NUMBER}")
            emailext(to: EMAIL_RECIPIENTS, subject: "Build ABORTED - ${env.JOB_NAME}", body: "Build ${env.BUILD_NUMBER} was aborted.")
        }
    }
}
