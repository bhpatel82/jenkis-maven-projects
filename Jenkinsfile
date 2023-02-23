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
        stage('Build & Dcoker Image') { 
            steps {
                sh 'docker built -t bhpatel82/maven_docker_jenkins_pipeline:${BUILD_NUMBER} .'
            }
        }
        stage('Dcoker login') { 
            steps {
                withCredentials([string(credentialsId: 'DockerID', variable: 'Dockerpwd')]){
                sh "docker login -u bhpatel82 -p ${Dockerpwd}"
                   }
            }
        }
        stage('Push to Repository') { 
            steps {
                sh 'docker push bhpatel82/maven_docker_jenkins_pipeline:${BUILD_NUMBER}'
            }
        }
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
    
