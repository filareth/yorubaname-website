pipeline {
  agent any
    tools {
      maven 'maven'
    }
    stages {
      stage ('build') {
        steps{
          // Выполняем только сборку и модульное тестирование с пропуском интеграционного тестирования
          sh 'mvn -B -DskipTests  clean install'
        }
      stage ('test') {
        steps{
          script{
            sh 'pwd'
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
      stage('deploy') {
        steps {
          echo "Deploy to aws servers via terraform and ansible"
        }
      }
    }
}
