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
          // Публикация отчетов модульных тестов JUnit
          junit '**/target/surefire-reports/TEST-*.xml'
          // Архивировать артефакты
          archiveArtifacts 'target/*.war'
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
      stage ('Static Code Analysis') {
        withSonarQubeEnv('my-sonarqube-demo') {
          sh 'mvn clean verify sonar:sonar -Dsonar.projectVersion=$BUILD_NUMBER'
        }
      }
      stage('deploy') {
        steps {
          echo "Deploy to aws servers via terraform and ansible"
        }
      }
    }
}
