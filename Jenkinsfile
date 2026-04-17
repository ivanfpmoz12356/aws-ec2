pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/ivanfpmoz12356/aws-ec2.git'
            }
        }

        stage('build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('test') {
            steps {
                sh 'npm test'
            }
        }

        stage('deploy') {
            steps {
                echo 'Deploy step (kasnije ćemo dodati pravi deploy)'
            }
        }
    }
}
