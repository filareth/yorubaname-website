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
      }
      stage ('test') {
        steps{
          script{
            sh 'sudo -i'
            sh 'pwd'
            sh 'cp /var/lib/jenkins/workspace/ekzamen/website/target/*.jar /home/ubuntu/'
            sh 'cd /home/ubuntu'
            sh 'git init'
            sh 'git config --global user.email "sobacka@gmail.com" && git config --global user.name "filareth"'
            sh ("git tag -a master-${env.BUILD_NUMBER} -m 'Artyfakt'")
            sh ('git push https://${GIT_USER_NAME}:${GIT_USER_PASSWORD}@${GIT_PROJECT_REPO}')
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
