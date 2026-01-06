pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/Swethapothuraju/finance/'
                 echo 'github url checkout'
            }
        }
        stage('codecompilet'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('code testing'){
            steps{
               echo 'Running unit tests with Maven'
               sh 'mvn -B -V test -Dmaven.test.failure.ignore=false'
            }
        }
        stage('qa'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8091:8091 --name c000 myimg'
            }
        }   
    }
}
