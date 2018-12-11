pipeline {
    agent any
    stages {
    
        stage('replace file') {
            steps {
                echo "replace config file use cp"
            } 
        }
        
        stage("unit test") {
            steps {
                echo "unit test"
            }
        }
        
        stage('package') {
            steps {
                sh 'tar czf /opt/web-${BUILD_ID}.tar.gz ./* --exclude=./git --exclude=Jenkinsfile'
            }
        }
        
        stage('deploy') {
            steps {
                sh 'ssh 10.0.0.11 "cd /var/www && mkidr web-${BUILD-ID}"'
                sh 'scp /opt/web-${BUILD_ID}.tar.gz 10.0.0.11:/var/www/web-${BUILD_ID}'
                sh 'ssh 10.0.0.11 "cd /var/www/web-${BUILD_ID} && tar xf web-${BUILD_ID}.tar.gz && rm -f web-${BUILD-ID}.tar.gz"'
                sh 'ssh 10.0.0.11 "cd /var/www && rm -rf html && ln -s /var/www/web-${BUILD_ID} /var/www/html"'
            }
        }
        
        stage('test') {
            steps {
                echo "deploy after test "
            }
        }
    }
}