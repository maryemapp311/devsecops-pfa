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

        stage('Docker Deploy') {
            steps {
                sh '''
                    docker rm -f netopshub || true
                    docker run -d \
                        --name netopshub \
                        -p 5000:5000 \
                        devsecops-pfa
                '''
            }
        }
    }
}
