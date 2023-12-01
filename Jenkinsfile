pipeline {
    agent any

    stages {
        stage('Clonar repositorio'){
            steps {
                git branch: 'main', 
                credentialsId: 'git-jenkins',
                url: 'https://github.com/victorcl15/api-rest-micro-tw.git' 
            }
        }
        stage('Construir imagen de docker'){

        }
        stage('Desplegar contenedor docker'){

        }
    }

    post {
        always {

        }
    }
}