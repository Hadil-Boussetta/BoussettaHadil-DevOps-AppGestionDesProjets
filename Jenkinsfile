
pipeline {
    agent any

    stages {
        stage('Checkout main') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Hadil-Boussetta/BoussettaHadil-DevOps-AppGestionDesProjets.git'
            }
        }

        stage('Maven compile') {
            steps {
                dir('backend') {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    dir('backend') {
                        sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=DevOps-AppGestionDesProjets'
                    }
                }
            }
        }

        stage('Build and Push Docker Images') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-hadil',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                            -u "$DOCKER_USERNAME" --password-stdin

                        docker build -t hadoull/devops-appgestiondesprojets-backend:1.0 ./backend
                        docker push hadoull/devops-appgestiondesprojets-backend:1.0

                        docker build -t hadoull/devops-appgestiondesprojets-frontend:1.0 ./frontend
                        docker push hadoull/devops-appgestiondesprojets-frontend:1.0

                        docker build -t hadoull/devops-appgestiondesprojets-db:1.0 ./database
                        docker push hadoull/devops-appgestiondesprojets-db:1.0
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Build succeeded: SonarQube analysis completed and Docker images were published.'
        }
        failure {
            echo 'Build failed. Check the Jenkins console output.'
        }
    }
}

