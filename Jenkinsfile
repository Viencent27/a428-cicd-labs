node {
  withCredentials([string(credentialsId: 'jenkins-github-token', variable: 'SECRET_VARIABLE')]) {
    env.PUBLIC_URL = 'https://viencent27.github.io/a428-cicd-labs'
    env.GITHUB_TOKEN = SECRET_VARIABLE
    env.GITHUB_REPOSITORY = 'Viencent27/a428-cicd-labs'
    withDockerContainer(image: 'timbru31/node-alpine-git:16', args: '-p 3000:3000') {
      stage('Build') {
        checkout scm
        sh 'npm install'
      }

      stage('Test') {
        sh './jenkins/scripts/test.sh'
      }

      stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy? (Klik "Abort" untuk mengakhiri)'
      }

      stage('Deploy') {
        sh './jenkins/scripts/deliver.sh'
        sleep(60)
        sh './jenkins/scripts/kill.sh'
        sh 'chmod +x ./jenkins/scripts/github-pages.sh && ./jenkins/scripts/github-pages.sh'
      }
    }
  }
}