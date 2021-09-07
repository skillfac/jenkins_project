pipeline {
    agent any

    stages {
        stage('first_query') {
            steps {
                sh(script:'''
         docker ps
        
        cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html
         
         docker run -dit --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest
         
          
          sh /home/ubuntu/script/1.sh
         
    
      
         # docker stop nginx
          #docker rm nginx 
               
               
               ''')
          
            }
        }
    }
}
