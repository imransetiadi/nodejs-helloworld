pipeline{
  environment {
    registry = "imransetiadi22/node-helloworld"
    registryCredential = 'dockerhub_credentials'
  }
  agent any
    stages {
        stage('Build'){
            steps{
                script{
                    sh 'npm install'
                }
            }
        }
        stage('Building image') {
            steps{
         
                echo 'Building..'
                sh 'docker image build -t $registry:${TAG} .'
                
             }
          }
          stage('Push Image') {
              steps{
                  script 
                    {
                        docker.withRegistry( '', registryCredential ) {
                            dockerImage.push()
                        }
                   } 
               }
            }
        stage('Deploying into k8s'){
            steps{
                sh 'kubectl apply -f deployment.yml'
            }
        }
    }
}
