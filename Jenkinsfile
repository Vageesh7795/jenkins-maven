pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                sh "mvn clean compile"
            }
        }
        stage('Test') { 
            steps {
                sh "mvn test site"
            }
            
             post {
                always {
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'   
                }
            }     
        }

        stage('deploy') { 
            steps {
                sh "mvn package"
            }
        }


        stage('Build Docker image'){
            steps {
                sh 'sudo docker build -t vageesh7795/docker_jenkins_pipeline:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Login'){
            
            steps {
                
                    sh 'sudo docker login -u vageesh7795 -p Vageesh@12'
            }                
        }

        stage('Docker Push'){
            steps {
                sh 'sudo docker push vageesh7795/docker_jenkins_pipeline:${BUILD_NUMBER}'
            }
        }
        
        stage('Docker deploy'){
            steps {
                sh 'sudo docker run -itd vageesh7795/docker_jenkins_pipeline:${BUILD_NUMBER}'
            }
        }

        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
