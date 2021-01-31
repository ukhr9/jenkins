pipeline {
    agent any
     environment {
        imageName = 'makevimage'
        BUILD_NUMBER = ''
        registryCredentialSet = 'dockerhub'
    }       

    stages {
       
        stage ('Build') {
            steps {
                script {
                    dockerInstance = docker.build${imageName}
                }
            }
        }

        stage ('Test') {
            steps {
                echo "Testing some config within built-in container..."
                script {
                    dockerInstance.inside('-u root')
                    echo "HELLO FROM INSIDE THE CONTAINER!!!"
                    sh 'timedatectl' 
                }
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
}