pipeline {
    agent any

    stages {
        stage('first_query') {
            steps {
                sh(script:'''
         
        
        cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html
         
         docker run  -d --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest
         
          echo "Testing the application in nginx container"
          
          docker exec -u 0 nginx  curl -LI http://127.0.0.1:80 -o /dev/null -w '%{http_code}\n' -s
          
          

          echo "Testing the application on the host system..."
                  
                  result=$(curl -LI http://127.0.0.1:9889 -o /dev/null -w '%{http_code}\n' -s)
                  echo $result
                  if [ "$result" = "200" ]
                  then
                      echo "Test passed"
                  else
                      echo "Test FAILURE"
                      exit 1
                  fi    
         
         
         echo "Checking integrity of files in container and on the host machine"
             
                     result1=$( curl -s  http://127.0.0.1:9889/index.html|md5sum | tr -d '( \-)')
                     result2=$( md5sum /var/lib/jenkins/workspace/proj/index.html)
                     echo $result1,$result2
                  if [ "$result1" = "$result2" ]
                  then
                      echo "Test passed"
                  else
                      echo "Test FAILURE"
                      exit 1
                  fi    
    
          
               
               
               ''')
                
                        
                    
            }
        }
    }
}
    
