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
    stage("version") {
      steps {
        script {
          def version = 1
          build = currentBuild.previousBuild
          while (build != null) {
            if (build == "SUCCESS") {
              version += 1
            }
          }
        }
      }
    }
    stage("build") {
      steps {
        sh " docker build -t stat-tag"
      }
    }
    stage("tag") {
      steps {
        sh "docker tag stat-tag janhvimaddeshiya/stat-tag:${version}"
  }
}
