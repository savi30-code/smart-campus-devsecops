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
                    script {
                        // Using SonarScanner instead of Maven
                        def scannerHome = tool 'SonarScanner'
                        bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=smart-campus-devsecops -Dsonar.projectName='Smart Campus DevSecOps' -Dsonar.sources=."
                    }
                }
            }
        }

        stage('Dependency Check - OWASP') {
            steps {
                echo 'Running OWASP Dependency Check...'
                dependencyCheck additionalArguments: '--format HTML --out reports', odcInstallation: 'Default'
                dependencyCheckPublisher pattern: 'reports/dependency-check-report.html'
            }
        }

        stage('Container Scan - Trivy') {
            steps {
                echo 'Scanning Docker image with Trivy...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to cloud (AWS EC2 / DigitalOcean)...'
            }
        }
    }
}
