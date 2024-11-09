pipeline {
    agent any

    tools {
        // Install the Maven version configured as "Maven-3" and add it to the path.
        maven "Maven-3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/DragoScript/COMP367-Lab3-Q1.git'

                // Run Maven with Jacoco on a Unix agent.
                sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }

        stage("Code Coverage") {
            steps {
                script {
                    // Publish Jacoco coverage report
                    sh "mvn org.jacoco:jacoco-maven-plugin:report"
                    jacoco(execPattern: 'target/**.exec')
                }
                
            }
        }
    }
}