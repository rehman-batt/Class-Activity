pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {

                git url: 'https://github.com/rehman-batt/Class-Activity.git'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    
                    sh 'docker login -u rehmanbatt -p u8UHqg3pmUFXKUL'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    
                    sh 'docker build -t class_activity_container .'
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    
                    sh 'docker tag class_activity_container rehmanbatt/class_activity_container'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    
                    sh 'docker push rehmanbatt/class_activity_container'
                }
            }
        }
    }

    post {
        always {
            sh 'docker image prune -f'
        }
        success {
            echo 'Docker image successfully pushed to Docker Hub!'
        }
        failure {
            echo 'Failed to push the Docker image.'
        }
    }
}
