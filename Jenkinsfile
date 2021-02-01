pipeline {
    agent { dockerfile true }
     environment {
        imageName = 'makevimage'
        BUILD_NUMBER = ''
        registryCredentialSet = 'dockerhub'
    }       

    stages {
       
        stage ('Build') {
            steps {
                script {
                    sh 'sudo docker build -t ${imageName}:latest .'   
                }
            }
        }    
    }
}