pipeline {
    agent any 
    stages {
        stage('SCM Checkout'){
            steps{
                git 'https://github.com/KrishnaGopalGupta/CI-CD-using-Docker.git'
            }
        }

        stage('Build APP'){
            steps {
                MVNHome = tool name: 'LocalMVN', type: 'maven'
                MVNCMD = "${MVNHome}/bin/mvn"
                sh "${MVNCMD} clean package"
            }
        }

        stage('Docker Build Tag'){
            steps{

                sh 'docker build -t krish0123/samplewebapp:latest .'
            }
        }

        stage('Docker push images') {

            steps{

                withCredentials([string(credentialsId: 'Docker_PWD', variable: 'Docker_pwd')]) {
                sh 'docker login -u krish0123 -p Krishna@123!@#'      
            }        

            sh 'docker push krish0123/samplewebapp:latest' 
       }
        
    }

    stage('Docker run application') {
        steps{
            sh "docker run -d -p 8003:8080 krish0123/samplewebapp:latest"
        }
     }
   }
}
