pipeline{ 
  agent any
  stages{
    stage( 'git scm update') {
      steps {
        git url: 'https://github.com/hw0915/cicdtest.git', branch: 'main'
      }
    }
  
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t heewon0915/cicdtest:green
        docker push heewon0915/cicdtest:green
        '''
      }
    }

    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deployment mypipe2 --image=heewon0915/cicdtest:green
        kubectl expose deploy mypipe2 --type=LoadBalancer --port=80 --target-port=80
        '''
      }
    }
  }
}

