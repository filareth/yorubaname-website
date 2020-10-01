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
            sh 'll'
            }
          }          
      post {
        success {
          echo "Success"
          }
        failure {
          echo "Failure"
          }
        }
      stage('deploy') {
        steps {
          echo "Deploy to aws servers via terraform and ansible"
          }
      }
    }
}
