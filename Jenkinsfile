pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    echo "Building the application..."
                    sh 'cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html'
                }
            }
        }
        stage('run_docker') {
            steps {
                script {
                    echo "Running the application..."
                    sh 'docker run  -d --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest'
                }
            }
        }
        stage('test_curl') {
            steps {
                sh(script:'''
                    echo "Testing the application..."
                  
                  result=curl -LI http://127.0.0.1:9889 -o /dev/null -w '%{http_code}\n' -s
                  echo $result
                  if [ "$result" = "200" ]
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
		    stage('test2') {
            steps {
                script {
                    echo "Deploying the application..."
					        sh 'docker stop nginx'
                  sh 'docker rm nginx'
                }
            }
        }
    }
}
