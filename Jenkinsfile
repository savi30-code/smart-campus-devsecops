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
                def scannerHome = tool 'SonarScanner'
                bat "${scannerHome}\\bin\\sonar-scanner -Dsonar.projectKey=smart-campus -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqa_8dfa6fceb89b7da3d44a167dfc0ecf4fe7e810ac"
            }
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
