pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/tnsdyd/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t mm0820/testweb:newnewmain .
        sudo docker push mm0820/testweb:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl set image deploy pod-main ctn-main=mm0820/testweb:newnewmain
        '''
      }
    }
  }
}
