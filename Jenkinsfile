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
                    sh 'docker build -t ${imageName}:latest'   
                }
            }
        }    
    }
}