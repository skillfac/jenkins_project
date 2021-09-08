pipeline {
    
    agent any
    
    stages {
        stage('1-Build') {
            steps {
                echo "Start of Stage Build..."
                sh 'cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html'
                sh 'docker run  -d --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest'
                echo "End of Stage Build..."
            }
        }
        stage('2-Test') {
            steps {
                echo "Start of Stage Test..."
                sh '''
                   result=$(curl -LI http://127.0.0.1:9889 -o /dev/null -w '%{http_code}\n' -s)
                  echo $result
                  if [ "$result" = "200" ]
                  then
                      echo "Test passed"
                  else
                      echo "Test FAILURE"
                      exit 1
                  fi    
                '''
             
                echo "End of Stage Build..."
                echo "End of Stage Build..."
            }
        }
        stage('3-Test') {
            steps {
                echo "Start of Stage Deploy..."
                echo "Deploying......."
                sh "ls -la"
                sh '''
                   result1=$( sudo curl -s  http://127.0.0.1:9889/index.html| md5sum |awk '{print $1}')
                     result2=$(  /var/lib/jenkins/workspace/proj/index.html | md5sum | awk '{print$1}')
                     echo $result1
                     echo $result2
                  if [ "$result1" = "$result2" ]
                  then
                      echo "Test passed"
                  else
                      echo "Test FAILURE"
                      exit 1
                  fi    
                   
                '''
                echo "End of Stage Build..."
            }
        }
        stage('4-Delete') {
            steps {
                sh 'docker stop nginx'
                sh 'docker rm nginx'
                
            }
        }	
    }
}
environment {
        EMAIL_TO = 'satanclaus617676@gmail.com'
    }
post {
        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        unstable {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
            emailext body: 'Check console output at $BUILD_URL to view the results.', 
                    to: "${EMAIL_TO}", 
                    subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
}
