pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t hello-saurabh:latest .'
                sh 'docker tag hello-saurabh:latest 8888998265/hello-saurabh:latest'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                      echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                      docker push 8888998265/hello-saurabh:latest
                    '''
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f hello-saurabh || true
                    docker run -d --name hello-saurabh -p 8081:8080 8888998265/hello-saurabh:latest
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Image built, pushed, and deployed successfully!"
        }
        failure {
            echo "❌ Something went wrong during the pipeline!"
        }
    }
}
