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
        stage("Sonar-scan") {
            steps {
                script {
                    
                    sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=Rajini@123"
                }

                }
            }
        
        stage('Build Docker Image') {
            steps {
                
                script {
      sh "docker build -t hello-world-java:${BUILD_NUMBER} ."
    
            }
        }
        }
    }
}
