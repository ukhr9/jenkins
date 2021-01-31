pipeline {
    agent any
     environment {
        imageName = 'mak3v/makevimage'
        BUILD_NUMBER = ''
        registryCredentialSet = 'dockerhub'
    }
    
    stages {
       
        stage ('Build') {
            steps {
                echo "Building container image..."
                script {
                    dockerInstance = docker.build($imageName)
                }
            }
        }

        stage ('Test') {
            steps {
                echo "Testing some config within built-in container..."
                script {
                    dockerInstance.inside('-u root')
                    sh 'echo "HELLO FROM INSIDE THE CONTAINER!!!"'
                    sh 'timedatectl' 
                }
                echo "Now we're inside of it, everything was ok."

            }

        }

        stage ('Deploy') {
            steps {
                echo "Deploying to mak3v dockerhub..."
                script {
                    docker.withRegistry('', registryCredentialSet) {
                    dockerInstance.push("${env.BUILD_NUMBER}")
                    dockerInstance.push("latest")
                }
            }
        }
    }
}