@Library('gitops-pipeline-library@v4') _

env.NAME = 'argo-rollouts'

switch(env.BRANCH_NAME) {
  case ~/PR-[0-9]+/: buildImage()
  break
  case 'skillz-master': buildImage()
  break
  case ~/fix-premature-canary-svc-labels-v0.10.2/: buildImage()
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
