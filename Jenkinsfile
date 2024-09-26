pipeline {
    agent any 

    environment {
        IMAGE_NAME = "sdev26/exam-jenkins-datascientest:${env.BUILD_ID}"
        DOCKER_REGISTRY = 'https://index.docker.io/v1/'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/s-dev26/Jenkins-Exam-DataScientest.git'
            }
        }

        stage('Check Docker') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} -f cast-service/Dockerfile ."

                    docker.withRegistry(DOCKER_REGISTRY, 'dockerhub-credentials') {
                        sh "docker push ${IMAGE_NAME}"
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    def namespace = 'dev'
                    if (env.BRANCH_NAME == 'master') {
                        namespace = 'prod'
                    } else if (env.BRANCH_NAME == 'staging') {
                        namespace = 'staging'
                    } else if (env.BRANCH_NAME == 'qa') {
                        namespace = 'qa'
                    }

                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
