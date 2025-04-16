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
            // Email with attachment for Unit and Integration Tests stage
            post{
                always{
                    script{
                        def testLog = currentBuild.rawBuild.getLog(1000).join("\n")
                        writeFile file: "console-test.log", text: testLog
                        archiveArtifacts artifacts: "console-test.log", allowEmptyArchive: true 
                        emailext(
                            to: "ollie.parks321@gmail.com",
                            subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                            body: "Unit and Integration Tests stage complete with status: ${currentBuild.currentResult}.",
                            attachmentsPattern: "console-test.log"
                        )
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
            // Email with attachment for Security Scan stage
            post{
                always{
                    script{
                        def secLog = currentBuild.rawBuild.getLog(1000).join("\n")
                        writeFile file: "console-security.log", text: secLog
                        archiveArtifacts artifacts: "console-security.log", allowEmptyArchive: true 
                        emailext(
                            to: "ollie.parks321@gmail.com",
                            subject: "Security Scan - ${currentBuild.currentResult}",
                            body: "Security Scan stage complete with status: ${currentBuild.currentResult}.",
                            attachmentsPattern: "console-security.log"
                        )
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
}