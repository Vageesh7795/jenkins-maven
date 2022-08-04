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
        }

        stage('deploy') { 
            steps {
                sh "mvn package"
            }
        }
            stage('Build Docker image'){
            steps {
                sh 'docker build -t vageesh7795/docker_jenkins_pipeline:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'vageesh7795', variable: 'Vageesh@12')]) {
                    sh "docker login -u vageesh7795 -p ${Vageesh@12}"
                }
            }                
        }

        stage('Docker Push'){
            steps {
                sh 'docker push vageesh7795/docker_jenkins_pipeline:${BUILD_NUMBER}'
            }
        }
        
        stage('Docker deploy'){
            steps {
                sh 'docker run -itd -p 8081:8080 vageesh7795/springboot:0.0.3'
            }
        }mm 
        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
