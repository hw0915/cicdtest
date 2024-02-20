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
        sudo docker build -t heewon0915/cicdtest:green .
        sudo docker push heewon0915/cicdtest:green
        '''
      }
    }

    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy myweb2 --image=heewon0915/cicdtest:green'
        ansible master -m command -a 'kubectl expose deploy myweb2 --type=LoadBalancer --port=80 --target-port=80' 
        '''
      }
    }
  }
}

