pipeline {
    agent any

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/psivaramps/<>.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("spamarthy/my-python-app:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'spamarthy') {
                        dockerImage.push()
                    }
                }
            }
        }


        stage('Run Container from Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'spamarthy') {  
                    docker.image("spamarthy/my-python-app:${env.BUILD_NUMBER}").run('-p 5001:5000 -d')
            }
        }
    }
}
          stage('Check Application with curl') {
            steps {
                script {
                    //sh "curl -f http://192.168.208.128/:5000"
                    sh "curl -f http://localhost:5001"  // Replace PORT and ENDPOINT
                        }
                    }
            }
    }
}

