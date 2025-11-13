pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/savi30-code/smart-campus-devsecops.git'
            }
        }

         stage('Code Scan - SonarQube') {
     steps {
        withSonarQubeEnv('SonarQubeServer') {
            bat 'mvn clean verify sonar:sonar -Dsonar.projectKey=smart-campus-devsecops -Dsonar.projectName="Smart Campus DevSecOps"'
        }
    }
}


        stage('Dependency Scan - OWASP') {
            steps {
                echo 'Running OWASP Dependency Check...'
            }
        }

        stage('Container Scan - Trivy') {
            steps {
                echo 'Scanning Docker image with Trivy...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to cloud (AWS EC2/DigitalOcean)...'
            }
        }
    }
}
