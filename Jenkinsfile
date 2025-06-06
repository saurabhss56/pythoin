pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repository...'
            }
        }

        stage('Run Script') {
            steps {
                sh 'python3 hello.py'
            }
        }
    }
}
