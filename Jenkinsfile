pipeline {
    agent any
    
    stages{
        stage("Stage 1: Build"){
            steps{
                echo "Compiling and packaging the code (e.g. using Maven)... "
                echo "Test for automatic polling"
            }
        }
        stage("Stage 2: Unit and Integration Tests"){
            steps{
                echo "Running tests (e.g. using JUnit)..."
            }
            // Writing the log for the test stage
            post{
                always{
                    script{
                        def testLog = Jenkins.instance.getItemByFullName(env.JOB_NAME)
                        .getBuildByNumber(env.BUILD_NUMBER.toInteger())
                        .getLog(1000)
                        .join("\n")
                        writeFile file: "console-test.log", text: testLog
                        archiveArtifacts artifacts: "console-test.log", allowEmptyArchive: true 
                    }
                }
            }
        }
        stage("Stage 3: Code Analysis"){
            steps{
                echo "Analyzing the code (e.g., with SonarQube)..."
            }
        }
        stage("Stage 4: Security Scan"){
            steps{
                echo "Scanning the code for vulnerabilities (e.g. with OWASP ZAP)..."
            }
            // Writing the log for the security scan stage
            post{
                always{
                    script{
                        def secLog = Jenkins.instance.getItemByFullName(env.JOB_NAME)
                        .getBuildByNumber(env.BUILD_NUMBER.toInteger())
                        .getLog(1000)
                        .join("\n")
                        writeFile file: "console-security.log", text: secLog
                        archiveArtifacts artifacts: "console-security.log", allowEmptyArchive: true 
                    }
                }
            }
        }
        stage("Stage 5: Deploy to Staging"){
            steps{
                echo "Deploying application to staging environment (e.g. AWS EC2)..."
            }
        }
        stage("Stage 6: Integration Tests on Staging"){
            steps{
                echo "Running integration tests in staging..."
            }
        }
        stage("Stage 7: Deploy to Production"){
            steps{
                echo "Deploying application to production environment (e.g. AWS EC2)..."
            }
        }
    }
    // Emailing the result and logs for test and security stage
    post{
        always{
            script{
                emailext(
                    to: "ollie.parks321@gmail.com",
                    subject: "Jenkins Pipeline - ${currentBuild.currentResult}",
                    body: "The Jenkins Pipeline for task 8.1C is complete with status: ${currentBuild.currentResult}. \nAttached are the logs for the test and security stages.",
                    attachmentsPattern: "console-*.log",
                    attachLog: false
                )
            }
        }
    }
}