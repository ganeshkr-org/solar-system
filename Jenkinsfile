pipeline {
    agent any
    tools {
        nodejs "nodejs-23-6-0"
    }

    stages {
        stage("Installing Dependencies") {
            steps {
                sh '''
                     node -v
                     npm -v
                     npm install --no-audit
                    '''
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

                        dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true 
                    }
                }
            }
        }
    }
}
