pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/shannu112/hello-world-cicd.git'
            }
        }

        stage('Deploy') {
            steps {

                sh '''

                ssh deploy@192.168.1.35 "
                sudo rm -rf /var/www/html/*
                "

                scp index.html deploy@192.168.1.35:/tmp/

                ssh deploy@192.168.1.35 "
                sudo mv /tmp/index.html /var/www/html/
                "

                '''
            }
        }

    }

}
