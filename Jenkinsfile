pipeline {
    agent any

    stages {
        stage('first_query') {
            steps {
                sh(script:'''
         docker ps
        
        cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html
         
         docker run -dit --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest
         
         curl 127.0.0.1:9889&&curl -LI 127.0.0.1:9889 -o /dev/null -w '%{http_code}\n' -s
    
        docker stop nginx&& docker rm nginx 
               
               
               ''')
          
            }
        }
    }
}
