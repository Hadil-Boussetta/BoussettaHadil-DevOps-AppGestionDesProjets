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
    }
}
