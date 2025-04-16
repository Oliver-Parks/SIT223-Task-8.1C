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
        }
        stage("Stage 3: Code Analysis"){
            steps{
                echo "Analyzing the code (e.g., with SonarQube)..."
            }
        }
        stage("Stage 4: Security Scan"){
            steps{
                echo "Scanning the code for vulnerabilities (e.g. with OWASP ZAP)..."
                // Capture output in a file
                sh 'echo "Security scan details..." > security.log'
                // Archive the artifact so Jenkins can access it later
                archiveArtifacts artifacts: 'security.log'
            }
            post{
                success{
                    emailext(
                        to: "ollie.parks321@gmail.com",
                        subject: "Security Scan Success"
                        body: "Security scan complete successfully, check attached log for details."
                        attachmentsPattern: 'security.log'
                    )
                }
                failure{
                    emailext(
                        to: "ollie.parks321@gmail.com",
                        subject: "Security Scan Failure"
                        body: "Security scan failed, check attached log for details."
                        attachmentsPattern: 'security.log'
                    )
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