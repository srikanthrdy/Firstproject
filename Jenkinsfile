pipeline {

    agent {
        
        label "master"
    }
    tools{
        maven "maven"
    }
    properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10']]]);, pipelineTriggers([githubPush()])])
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
      sh "$docker_path/docker build -t np:${BUILD_NUMBER} ."
    
            }
        }
        }
        stage("archiveArtifacts") {
            steps {
                   archiveArtifacts artifacts: 'target/np.jar', followSymlinks: false
            }
        }
         stage("clean Workspace") {
            steps {
                    cleanWs()
            }
         }
        
    }
}
