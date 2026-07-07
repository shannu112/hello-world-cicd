pipeline {

    agent any

    environment {

        IMAGE="shanmugha/hello-world"

    }

    stages {

        stage('Build') {

            steps {

                sh '''

                docker build -t $IMAGE:latest .

                '''
            }

        }

        stage('Login') {

            steps {

                withCredentials([usernamePassword(credentialsId: 'dockerhub',

                usernameVariable: 'USER',

                passwordVariable: 'PASS')]) {

                sh '''

                echo $PASS | docker login -u $USER --password-stdin

                '''

                }

            }

        }

        stage('Push') {

            steps {

                sh '''

                docker push $IMAGE:latest

                '''
            }

        }

        stage('Deploy') {

            steps {

                sh '''

                ssh deploy@192.168.1.35 "

                docker pull $IMAGE:latest

                docker compose down

                docker compose up -d

                "

                '''

            }

        }

    }

}