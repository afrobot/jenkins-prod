#!/usr/bin/env groovy

 devRepo = 'git@github.com:afrobot/jenkins-dev.git'
prodRepo = 'git@github.com:afrobot/jenkins-prod.git'

node {
  stage 'checkout'
    checkoutRepo(devRepo, prodRepo)
    checkout scm
    
    // git url: "${prodRepo}", credentialsId: 'github-afrobot', name: 'prod'

  stage 'build'
    sshagent(['github-afrobot']) {
      sh """
        git fetch --all
        git show-ref
        git branch
        git diff origin/master
        git ls-remote
      """ }

}



// stage 'build'
//   node {
//     //checkout scm
//     sshagent(['github-afrobot']) {
//       git url: 'git@github.com:afrobot/jenkins-dev.git', credentialsId: 'github-afrobot', name: 'origin'
//
//       addRemoteRepo(prodRepo)
//
//       sh """
//         git fetch --all
//         git show-ref
//         git branch
//         git diff origin/master
//         git ls-remote
//       """
//     }
//   }
//   }
//
def checkoutRepo(devRepo, prodRepo) {
  checkout([
    $class:'GitSCM',
    branches: [[name: 'master']],
    userRemoteConfigs: [
      [credentialsId: 'github-afrobot', url: "${devRepo}",  name: 'origin'],
      [credentialsId: 'github-afrobot', url: "${prodRepo}", name: 'prod']
    ]])
}

// git fetch --all
// git show-ref
// git branch
// git diff origin/master
// git ls-remote
