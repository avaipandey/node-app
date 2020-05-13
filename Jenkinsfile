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
                 withCredentials([file(credentialsId: 'jacc', variable: 'gke')]) {
                   
                     sh("gcloud auth activate-service-account --key-file '${gke}'")
                     sh("gcloud container clusters get-credentials cluster-1 --zone us-central1-a --project robotic-tract-277114")
                     sh "gcloud compute scp --strict-host-key-checking=no ~/serivces.yml ~/pods.yml jenkins1@robotic-tract-277114.iam.gserviceaccount.com/home/jenkins1/ --zone=us-central1-a"
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
