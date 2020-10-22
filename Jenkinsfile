pipeline {

  environment {
   registry = "192.168.1.81:5000/justme/myweb"
   dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/gvgiri/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build gvgiri/example-repo:3.0"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

   stage('Deploy App') {
     steps {
        script {
          kubernetesDeploy(configs: "myweb2.yaml", kubeconfigId: "mykubeconfig2")
        }
      }
    }

  }

}
