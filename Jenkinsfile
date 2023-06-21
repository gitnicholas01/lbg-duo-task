pipeline {
    agent any
         
    stages {
        
       
        stage('Build') {
            steps {
                sh 'docker build -t duo-task:v1 .'
            }
        }
        stage('run containers') {
            steps {
                sh '''
                docker network inspect duo-net && sleep 1 || docker network create duo-net
                docker run -d --name flask-app --network duo-net duo-task:v1
                docker run -d -p 80:80 --network duo-net mount type=bind,source=$(pwd)/nginx.conf,target=etc/nginx/nginx.conf --name nginx nginx:alpine
                '''
            }
        }
    }
}
