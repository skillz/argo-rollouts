@Library('gitops-pipeline-library@v4') _

env.NAME = 'game-play-service'

switch(env.BRANCH_NAME) {
  case ~/PR-[0-9]+/: buildImage()
  break
  case 'skillz-master': buildImage()
  break
}

def buildImage() {
  workerTemplates.docker {
    node(POD_LABEL) {
      container('docker') {
        def scmVars =  checkout(scm)
        def imageTag = scmVars.GIT_COMMIT
        dockerBuildPush(tag: imageTag)
      }
    }
  }
}
