pipeline {
    agent any

    stages {
        stage('first_query') {
            steps {
                sh(script:'''
         docker ps
         docker run -dit --name nginx -v /home/ubuntu/www/html:/var/www/html -p9889:80 nginx:latest
         
               
               
               ''')
          
            }
        }
    }
}
