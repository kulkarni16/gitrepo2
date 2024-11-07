pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/kulkarni16/gitrepo2', branch: 'main', credentialsId: '969e90cd-787d-455d-b644-919635241dd4')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t kulkarni16/srepo1:latest .
sudo docker push kulkarni16/srepo1:latest'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 kulkarni16/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 kulkarni16/srepo1:latest'''
          }
        }

      }
    }

  }
}