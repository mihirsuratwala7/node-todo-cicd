pipeline {  
    agent { label 'node-agent1' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/mihirsuratwala7/node-todo-cicd.git', branch: 'master' 
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t mihirsuratwala13/node-cicd-pipeline:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push mihirsuratwala13/node-cicd-pipeline:latest'
                }
            }
        }
        stage('Test'){
            steps{
                echo "Testing the new build"
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d --no-deps --build web"
            }
        }
    }
}
