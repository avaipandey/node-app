pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
       
    }
    stages{
        stage('Build Docker Image'){
            steps{
               
                  
                      sh "docker build . -t avaipandey/nodeapp:${DOCKER_TAG}"
                  
              
            }
        }
        stage('Pushing Docker Image'){
            steps{
               
                       sh "docker login -u avaipandey -p Docker#456456456  avaipandey/nodeapp:${DOCKER_TAG}"
                      sh "docker push  avaipandey/nodeapp:${DOCKER_TAG}"
                  
              
            }
        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
