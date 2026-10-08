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
                    sh './mvnw clean compile'
                }
            }
        }

        stage('Docker build and push') {
            steps {
                dir('backend') {
                    sh 'docker build -t hadoull/devops-appgestiondesprojets-backend:1.0 .'
                    sh 'docker push hadoull/devops-appgestiondesprojets-backend:1.0'
                }
            }
        }
    }
}
