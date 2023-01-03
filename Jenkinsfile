pipeline{
    environment{
        IMAGE_NAME="mohammadathar/todo"
        dockerImage=''
        DOCKER_C='docker_credentials'
    }
    agent any
    stages{
        stage('Building Image'){
            steps{
                // using docker pipeline plugin
                script{
                     dockerImage = docker.build env.IMAGE_NAME

                }
            }
        }
        stage('pushing image to dockerhub'){
            steps{
                script{   
                docker.withRegistry('', env.DOCKER_C){
                    dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy to K8s')
  {
   steps{
   	sh 'docker run -d -p 3000:3000 env.IMAGE_NAME'
     }
    }
   }
  }
    }
}
