pipeline {
    agent any 
    stages {
        stage('Compile and Clear') { 
            steps {
               sh "mvn clean Compile"
            }
        }
        stage('Test') { 
            steps {
                sh "mvn test" 
            }
        }
        stage('Deploy') { 
            steps {
                sh "mvn package" 
            }
        }
    }
}
