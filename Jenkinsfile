pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                echo 'build'
                sh 'cp /var/lib/jenkins/workspace/proj/index.html /home/ubuntu/www/html/index.html'
            }
        }
    } 
        stage('run') {
            steps {
                echo 'Starting the docker'
                sh 'docker run  -d --name nginx -v /home/ubuntu/www/html:/usr/share/nginx/html -p9889:80 nginx:latest'
            }
        }
    }
        stage('test') {
            steps {
                echo 'Test'
                sh ('''
                  
                  result=$(curl -LI http://127.0.0.1:9889 -o /dev/null -w '%{http_code}\n' -s)
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
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }

}
