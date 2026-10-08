pipeline {

    agent any

    stages {

        // Stage 1 : récupérer le projet depuis GitHub
        stage('Checkout main') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Hadil-Boussetta/BoussettaHadil-DevOps-AppGestionDesProjets.git'
            }
        }

        // Stage 2 : compiler le backend et générer le fichier JAR
        stage('Maven compile') {
            steps {
                dir('backend') {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        // Stage 3 : construire et publier l'image Docker
        stage('Docker build and push') {
            steps {
                dir('backend') {
                    withCredentials([usernamePassword(
                        credentialsId: 'dockerhub-hadil',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )]) {

                        // Connexion à Docker Hub
                        sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'

                        // Construction de l'image Docker
                        sh 'docker build -t hadoull/devops-appgestiondesprojets-backend:1.0 .'

                        // Publication de l'image sur Docker Hub
                        sh 'docker push hadoull/devops-appgestiondesprojets-backend:1.0'
                    }
                }
            }
        }
    }
}
