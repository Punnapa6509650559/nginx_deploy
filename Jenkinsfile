pipeline {

    agent any 



    stages {

        stage('Checkout Code') {

            steps {

                git branch: 'main', url: 'https://github.com/Punnapa6509650559/nginx_deploy' 

            }

        }



        stage('Build Docker Image') {

            steps {

                script {

                    docker.build("my-nginx-app:${env.BUILD_NUMBER}")

                }

            }

        }



        stage('Deploy Nginx Container') {

            steps {

                script {

                    sh "docker stop my-nginx-container || true"

                    sh "docker rm my-nginx-container || true"

                    docker.run("-p 8091:80 --name my-nginx-container", "my-nginx-app:${env.BUILD_NUMBER}")

                }

            }

        }

    }



    post {

        always {

            echo "Pipeline finished."

        }

        success {

            echo "Deployment successful!"

        }

        failure {

            echo "Deployment failed!"

        }

    }

}
