//def lastSuccessfulBuildID = 0
//def version = 0
//def buildNumber = currentBuild.number
//def build = currentBuild.previousBuild
//if (build == null) {
 //  version = 1
//}
//while (build != null) {
    //if (build.result == "SUCCESS") {
        //lastSuccessfulBuildID = build.id as Integer
        //version = lastSuccessfulBuildID + 1
      //  break
    //} else if(build.result == "FAILURE") {
        //lastSuccessfulBuildID = build.id as Integer
      //  version = lastSuccessfulBuildID - buildNumber
    //}
  //  build = build.previousBuild
//}

pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    KUBECONFIG = credentials('kubeconfig')
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
    //stage("Log-in") {
      //steps {
        //sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      //}
    //}
    stage("build") {
      steps {
        sh " docker build -t janhvimaddeshiya/stat-tag Static-website/"
      }
    }
    //stage("Push-repo") {
      //steps {
        //sh "docker push janhvimaddeshiya/stat-tag:${version}"
      //}
    //}
     stage("apply kube") {
      steps {
        sh "kubectl --kubeconfig $KUBECONFIG apply -f Static-website/deploy.yaml"
      }
    }
  }
}
