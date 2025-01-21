pipeline {
    agent any
    tools {
        nodejs "nodejs-23-6-0"
    }

    stages {
        stage("Installing Dependencies") {
            steps {
<<<<<<< HEAD
                sh  '''
                     node -v
                     npm -v
                     npm install --no-audit
                    '''
=======
                sh '''
                     node -v
                     npm -v
                     npm install --no-audit
                   '''
>>>>>>> e934eea73fff471c55ef4dd770e8543df91a9c03
            }
        }

        stage("Dependency Scanning") {
            parallel {
                stage("NPM Dependency Audit") {
                    steps {
                        sh 'npm audit --audit-level=critical'
                    }
                }

                stage("OWASP Dependency Checks") {
                    steps {
                        dependencyCheck additionalArguments: '''
                            --scan \'./\' 
                            --out \'./\' 
                            --format \'ALL\' 
                            --prettyPrint 
                            --nvdCveApiKey 6aecb2fd-1f4a-49aa-aa24-c22987a2c366
                        ''', 
                        odcInstallation: 'OWASP DepCheck 10'
<<<<<<< HEAD

                        dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true 
=======
                        dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true      
>>>>>>> e934eea73fff471c55ef4dd770e8543df91a9c03
                    }
                }
            }
        }
    }
}
