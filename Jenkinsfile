pipeline {

    agent {
        
        label "master"
    }
    tools{
        maven "maven"
    }
    stages {

        stage("Maven Build") {
            
            steps {

                script {
                sh "mvn package -DskipTests=true"
                }
                }

            }
       stage("SonarQube Analysis") {
            steps {
                withSonarQubeEnv('sonar') {
                sh 'mvn sonar:sonar'
                  }
             }
           } 
        
        stage('Build Docker Image') {
            steps {
                
                script {
      sh "$docker_path/docker build -t hello-world-java:${BUILD_NUMBER} ."
    
            }
        }
        }
    }
}
