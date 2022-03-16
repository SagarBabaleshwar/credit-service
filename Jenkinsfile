node{
  def MAVEN_HOME = tool "mymaven"
  env.PATH = "${env.PATH}:${MAVEN_HOME}/bin"
  stage('checkout'){
  checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SagarBabaleshwar/credit-service.git']]])
  }
  stage('initial set up'){
  sh('mvn clean compile')
  }
  stage('run test'){
  sh('mvn test')
  }
}
