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

        stage('Docker build and push') {
            steps {
                dir('backend') {
                    withCredentials([usernamePassword(
                        credentialsId: 'dockerhub-hadil',
                        usernameVariable: 'hadoull',
                        passwordVariable: 'Baba220701//'
                    )]) {

                        sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                        sh 'docker build -t hadoull/devops-appgestiondesprojets-backend:1.0 .'
                        sh 'docker push hadoull/devops-appgestiondesprojets-backend:1.0'
                    }
                }
            }
        }
    }
}
