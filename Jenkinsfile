node{
  stage('checkout'){
  checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SagarBabaleshwar/credit-service.git']]])
  }
  stage('initial set up'){
  sh('mvn clean compile')
  }
}
