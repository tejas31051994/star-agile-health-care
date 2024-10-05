pipeline {
  agent any
     tools {
       maven 'M2_HOME'
           }
 
  stages {
    stage('Git Checkout') {
      steps {
        echo 'This stage is to clone the repo from github'
        git branch: 'master', url: 'https://github.com/tejas31051994/star-agile-health-care.git'
                        }
            }
    stage('Create Package') {
      steps {
        echo 'This stage will compile, test, package my application'
        sh 'mvn package'
                          }
            }
    stage('Generate Test Report') {
      steps {
        echo 'This stage generate Test report using TestNG'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Healthcare/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                          }
            }
    stage('Create Docker image') {
      steps {
        echo 'This stage will create docker image'
        sh 'docker build -t tejtejas/healthcare:1.0 .'
                          }
            }
    stage('Login to Dockerhub') {
      steps {
        echo 'This stage will loginto dockerhub'
        withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'dockeruser', usernameVariable: 'dockeruser')]) {
        sh 'docker login -u ${dockeruser} -p ${dockeruser}'
            } 
      }
  }
  stage('Docker Push-Image') {
      steps {
        echo 'This stage will push my new image to the dockerhub'
        sh 'docker push tejtejas/healthcare:1.0'
            }
        }
      }
}
