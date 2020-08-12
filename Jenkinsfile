pipeline {

    environment {
        /* Provide the docker credential name in the Jenkins server */
        registryCredential = 'docker-hub-credentials'

        /* Define the variable of docker image */
        dockerImage = ''
    }

    agent {
        /* Specify the slave node via docker engine */
        label 'slave'
    }

    stages {

        stage('Clone repository') {
            /* Make sure the repository cloned to the workspace */
            steps{
                git 'https://github.com/mohammadhoseinchahardoli/sample-fibonacci'
            }
        }

        stage('Build and Test Frontend') {
            steps{
                script{
                    /* Build the Frontend docker image */
                    dockerImage = docker.build "chahardoli/fibo-frontend:test", "-f ./frontend/Dockerfile.dev ./frontend"
                    sh "docker run -e CI=true chahardoli/fibo-frontend:test npm test"
                }
            }
        }

        stage('Remove Unused test Frontend docker image') {
            steps{
                /* Clean the Frontend docker image from slave */
                sh "docker rmi -f chahardoli/fibo-frontend:test"
            }
        }

        stage('Build Frontend') {
            steps{
                script{
                    /* Build the Frontend docker image */
                    dockerImage = docker.build "chahardoli/fibo-frontend", "-f ./frontend/Dockerfile ./frontend"
                }
            }
        }

        stage('Push Frontend Image'){
            steps{
                script{
                    /* Push the Frontend docker image via Git SHA and latest tags */
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("latest")
                        dockerImage.push("${env.GIT_COMMIT}")
                    }
                }
            }
        }

        stage('Remove Unused Frontend docker image') {
            steps{
                /* Clean the Frontend docker image from slave */
                sh "docker images | grep fibo-frontend | tr -s ' ' | cut -d ' ' -f 2 | xargs -I {} docker rmi -f chahardoli/fibo-frontend:{}"
            }
        }

        stage('Build Backend') {
            steps{
                script{
                    /* Build the Backend docker image */
                    dockerImage = docker.build "chahardoli/fibo-backend", "-f ./backend/Dockerfile ./backend"
                }
            }
        }

        stage('Push Backend Image'){
            steps{
                script{
                    /* Push the Backend docker image via Git SHA and latest tags */
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("latest")
                        dockerImage.push("${env.GIT_COMMIT}")
                    }
                }
            }
        }

        stage('Remove Unused Backend docker image') {
            steps{
                /* Clean the Backend docker image from slave */
                sh "docker images | grep fibo-backend | tr -s ' ' | cut -d ' ' -f 2 | xargs -I {} docker rmi chahardoli/fibo-backend:{}"
            }
        }

        stage('Build Worker') {
            steps{
                script{
                    /* Build the Worker docker image */
                    dockerImage = docker.build "chahardoli/fibo-worker", "-f ./worker/Dockerfile ./worker"
                }
            }
        }

        stage('Push Worker Image'){
            steps{
                script{
                    /* Push the Worker docker image via Git SHA and latest tags */
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("latest")
                        dockerImage.push("${env.GIT_COMMIT}")
                    }
                }
            }
        }

        stage('Remove Unused Worker docker image') {
            steps{
                /* Clean the Worker docker image from slave */
                sh "docker images | grep fibo-worker | tr -s ' ' | cut -d ' ' -f 2 | xargs -I {} docker rmi chahardoli/fibo-worker:{}"
            }
        }

        stage('Build Nginx') {
            steps{
                script{
                    /* Build the Nginx docker image */
                    dockerImage = docker.build "chahardoli/fibo-nginx", "-f ./nginx/Dockerfile ./nginx"
                }
            }
        }

        stage('Push Nginx Image'){
            steps{
                script{
                    /* Push the Nginx docker image via Git SHA and latest tags */
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("latest")
                        dockerImage.push("${env.GIT_COMMIT}")
                    }
                }
            }
        }

        stage('Remove Unused Nginx docker image') {
            steps{
                /* Clean the Nginx docker image from slave */
                sh "docker images | grep fibo-nginx | tr -s ' ' | cut -d ' ' -f 2 | xargs -I {} docker rmi chahardoli/fibo-nginx:{}"
                sh "docker image prune -f "
            }
        }
    }
}
