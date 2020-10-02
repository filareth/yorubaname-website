pipeline {
  agent any
    tools {
      maven 'maven'
    }
    stages {
      stage ('build') {
        steps{
          sh 'mvn -B -DskipTests  clean install'
          }
        }
      stage ('test') {
        steps{
          script{
            sh 'ls -ln'
            }          
        post {
          success {
            echo "Success"
          }
        failure {
          echo "Failure"
          }
        }
      }
    }
      stage('Copy Archive') {
            steps {
              script {
                step ([$class: 'CopyArtifact',
                    projectName: 'ekzamen',
                    filter: "ekzamen*.zip",
                    target: '.']);
              }
            }
          }
      stage('deploy') {
        steps {
          echo "Deploy to aws servers via terraform and ansible"
        }
      }
    }
}
