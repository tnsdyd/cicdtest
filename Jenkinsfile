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
	sudo sed -e "s\$/text/" index.html
        sudo docker build -t mm0820/testweb:newnewblog .
        sudo docker push mm0820/testweb:newnewblog
	sudo sed 's\$/ttt/' index.html
	sudo docker build -t mm0820/testweb:newnewshop .
	sudo docker push mm0820/testweb:newnewshop
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl set image deploy pod-blog ctn-blog=mm0820/testweb:newnewblog
	sudo kubectl set image deploy pod-shop ctn-shop=mm0820/testweb:newnewshop
        '''
      }
    }
  }
}
