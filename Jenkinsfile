pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                echo 'NetOpsHub CI/CD fonctionne !'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t devsecops-pfa .'
            }
        }
    }
}
