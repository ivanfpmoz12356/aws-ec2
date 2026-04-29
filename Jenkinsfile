pipeline {
    agent any

    environment {
        APP_HOST = '52.201.150.125'
        APP_USER = 'ubuntu'
        APP_DIR  = '/home/ubuntu/app'
    }

    stages {

        stage('checkout') {
            steps {
                checkout scm
            }
        }

        stage('build') {
            steps {
                sh 'npm install'
            }
        }

        stage('test') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('deploy') {
            steps {
                sh """
                    ssh -o StrictHostKeyChecking=no ${APP_USER}@${APP_HOST} 'mkdir -p ${APP_DIR}'

                    rsync -avz --delete ./ ${APP_USER}@${APP_HOST}:${APP_DIR}/

                    ssh -o StrictHostKeyChecking=no ${APP_USER}@${APP_HOST} '
                        cd ${APP_DIR} &&
                        npm install &&
                        pm2 delete app || true &&
                        pm2 start app.js --name app &&
                        pm2 save
                    '
                """
            }
        }
    }
}
