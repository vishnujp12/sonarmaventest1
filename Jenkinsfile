pipeline {
    agent {
        docker {
            image 'buildcontainer:3.0'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code inside the Docker container
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run the Python script without changing the directory
                sh "python3 /app/g1.py"
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    // Run SonarQube analysis
                    withSonarQubeEnv('sonarqube') {
                        sh 'mvn clean install sonar:sonar'
                    }
                }
            }
        }
    }
}
