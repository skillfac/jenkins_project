pipeline {
    agent any

    stages {
        stage('first_query') {
            steps {
                sh(script:'''
         docker ps
        
        cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html
         
         docker run -dit --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest
         
          
          response=`curl -k -s -X GET --url "<127.0.0.1:9889>"`
          echo "${response}"
         
    
      
          docker stop nginx&& docker rm nginx 
               
               
               ''')
          
            }
        }
    }
}
