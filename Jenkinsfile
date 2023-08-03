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
    stage("version") {
      steps {
        script {
          def version = 1
          build = currentBuild.previousBuild
          while (build != null) {
            if (build == "SUCCESS") {
              version += 1
              break
            }
            build = build.previousBuild
          }
        }
      }
    }
    stage("build") {
      steps {
        sh " docker build -t stat-tag Static-website/"
      }
    }
    stage("tag") {
      steps {
        sh "docker tag stat-tag janhvimaddeshiya/stat-tag:${version}"
      }
    }
    stage("Push-repo") {
      steps {
        sh "docker push janhvimaddeshiya/stat-tag:${version}"
      }
    }
  }
}
