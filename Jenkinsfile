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

                    sleep 5
                '''
            }
        }

        stage('OWASP ZAP Security Scan') {
            steps {
                sh '''
                    docker run --rm \
                        --network host \
                        --user root \
                        -v "$WORKSPACE:/zap/wrk/:rw" \
                        ghcr.io/zaproxy/zaproxy:stable \
                        zap-baseline.py \
                        -t http://127.0.0.1:5000 \
                        -r zap-report.html \
                        -J zap-report.json || true
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'zap-report.html,zap-report.json',
                             allowEmptyArchive: true
        }
    }
}
