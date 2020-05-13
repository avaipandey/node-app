pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
       
    }
    stages{
        stage('Build Docker Image'){
            steps{
                withCredentials([string(credentialsId: 'docerpwd', variable: 'dockerpwd')]) {
                    sh "docker login -u dockeradmin -p ${dockerpwd}"
                      sh "docker build . -t avaipandey/nodeapp:${DOCKER_TAG}"
                  }
              
            }
        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
