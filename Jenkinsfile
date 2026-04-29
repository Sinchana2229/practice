pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Sreevathsa67/ht.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t sreevathsa221/htmlstatic ."
            }
        }

      stage('Push to Docker Hub') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub',
        usernameVariable: 'USER',
        passwordVariable: 'PASS')]) {

            bat "docker login -u %USER% -p %PASS%"
            bat "docker push sreevathsa221/htmlstatic:latest"
        }
    }
}

        stage('Run Container') {
            steps {
                bat "docker run -d -p 8080:80 sreevathsa221/htmlstatic"
            }
        }
    }
}
