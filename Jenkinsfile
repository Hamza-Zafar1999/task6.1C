pipeline {
    
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build'
                echo 'Task: Compile and build the code'
                echo 'Tools: Bazel, SBT, Make'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'h.zafar112233@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Build Stage",
                            body: "Build failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests'
                echo 'Task: Execute unit and integration tests'
                echo 'Tools: PyTest, Mocha, Jasmine'
                sh 'echo "Running unit and integration tests..." > unit-integration-tests.log'
                sh 'echo "Tests successfully completed." >> unit-integration-tests.log'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Quality Analysis'
                echo 'Task: Analyze the code for maintainability and best practices'
                echo 'Tools: ESLint, TSLint, PHPStan'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'h.zafar112233@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Code Analysis Stage",
                            body: "Code analysis failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Vulnerability Scan'
                echo 'Task: Perform security checks on the codebase'
                echo 'Tools: Bandit, TruffleHog, Whitesource'
                sh 'echo "Performing security scan..." > security-checks.log'
                sh 'echo "Security scan finished." >> security-checks.log'
            }
            post {
                always {
                    script {
                        def buildStatus = currentBuild.result ?: 'SUCCESS'
                        def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Security Scan ${buildStatus}"
                        def body = """
                        Security Scan Status: ${buildStatus}
                        Job: ${env.JOB_NAME}
                        Build Number: ${env.BUILD_NUMBER}
                        """
                        emailext (
                            to: 'h.zafar112233@gmail.com',
                            subject: subject,
                            body: body,
                            attachmentsPattern: 'security-checks.log'
                        )
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Staging Deployment'
                echo 'Task: Deploy the application to the staging environment'
                echo 'Tools: Heroku, Vagrant, Terraform'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'h.zafar112233@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Deploy to Staging Stage",
                            body: "Deployment to staging failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Staging Integration Tests'
                echo 'Task: Run integration tests in the staging environment'
                echo 'Tools: Robot Framework, TestCafe, JMeter'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'h.zafar112233@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Integration Tests Stage",
                            body: "Integration tests on staging failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Production Deployment'
                echo 'Task: Deploy the application to the production environment'
                echo 'Tools: Jenkins X, Capistrano, Flyway'
            }
            post {
                failure {
                    script {
                        emailext (
                            to: 'h.zafar112233@gmail.com',
                            subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Deploy to Production Stage",
                            body: "Deployment to production failed. Please check the logs for details.",
                            attachLog: true
                        )
                    }
                }
            }
        }
    }
    post {
        always {
            script {
                def buildStatus = currentBuild.result ?: 'SUCCESS'
                def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - ${buildStatus}"
                def body = """
                Build Status: ${buildStatus}
                Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                """
                emailext (
                    to: 'h.zafar112233@gmail.com',
                    subject: subject,
                    body: body,
                    attachLog: true
                )
            }
        }
    }
}
