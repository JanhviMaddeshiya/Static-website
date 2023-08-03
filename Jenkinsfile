pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage("Clean-up") {
      steps {
        deleteDir()
      }
    }
    stage("clone repo") {
      steps {
        sh "git clone https://github.com/JanhviMaddeshiya/Static-website"
      }
    }
    stage("Log-in") {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage("build") {
      steps {
        sh " docker build -t janhvimaddeshiya/stat-tag Static-website/"
      }
    }
    stage("Push-repo") {
      steps {
        sh "docker push janhvimaddeshiya/stat-tag"
      }
    }
    stage('Deploying to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml")
        }
      }
    }
  }
}
