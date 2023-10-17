node {
  withDockerContainer(image: 'node:16-buster-slim', args: '-p 3000:3000') {
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
    }
  }
}