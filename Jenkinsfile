pipeline {
    agent any

    stages {
        stage('first_query') {
            steps {
                sh(script:'''
         
        
        cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html
         
         docker run  -d --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest
         
          
           curl -I http://localhost:9889
          
         
    
      
          
               
               
               ''')
          
            }
        }
    }
}
