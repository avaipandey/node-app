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
                withCredentials([string(credentialsId: 'Dockerhub', variable: 'hubpw')]) {
                    sh "docker login -u avaipandey -p ${hubpw}"
                      sh "docker push  avaipandey/nodeapp:${DOCKER_TAG}"
                 }
               
                   
                  
              
            }
        }
         stage('Deploy to GKE Docker Image'){
            steps{
                 withCredentials([file(credentialsId: 'gke', variable: 'gke')]) {
                     sh("gcloud auth activate-service-account --key-file=${gke}")
                     sh("gcloud container clusters get-credentials cluster-1 --zone us-central1-a --project robotic-tract-277114")
                     sh "kubectl apply -f"
                  }
               
                   
                  
              
            }
        }
       
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
