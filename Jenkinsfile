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
            steps {
                script {
                    withCredentials([
                       string(credentialsId: 'MONGO_DB_URI', variable: 'MONGO_DB_URI')
                    ]) {
                        sh """
                            docker build --build-arg MONGO_DB_URI=${MONGO_DB_URI} -t loader-balancer:v1 .
                            """  
                        //docker.build('loader-balancer:v1', "--build-arg MONGO_DB_URI=${MONGO_DB_URI} .")

                        }
                    
                    
                }
            }
        }
        stage('Desplegar contenedor docker'){
            steps {
               script {
                    withCredentials([
                       string(credentialsId: 'MONGO_DB_URI', variable: 'MONGO_DB_URI')
                    ]) {
                       /* sh """
                            sed '${MONGO_DB_URI}' docker-compose.yml > docker-compose-updated.yml
                            docker-compose -f docker-compose-updated.yml up -d
                        """*/
                        sh """
                            docker-compose -f docker-compose.yml up -d
                        """

                        }
                    
                    
                } 
            }
        }
    }

    /*post {
        always {
            emailext {
                subject: "Estado del build: ${currentBuild.currentResult}",
                body: "Se ha completado el build, accede a los detalles en ${env.BUILD_URL}",
                to: 'victorcl2002@gmail.com',
                cc: 'victorclgames15@gmail.com',
                from: 'jenkins@iudigital.edu.co'
            }
        }
    }*/
}