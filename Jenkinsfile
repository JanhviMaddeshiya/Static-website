pipeline {
  agent any
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
  }
}
