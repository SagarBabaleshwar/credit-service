podTemplate(cloud: 'kubernetes',label: 'kubernetes',
            containers: [
                    containerTemplate(name: 'podman', image: 'quay.io/containers/podman', privileged: true, command: 'cat', ttyEnabled: true)
					
            ]) 
{
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
  stage('Code Quality Analysis'){    
    withSonarQubeEnv('sagarsonar'){
                 sh 'mvn sonar:sonar -Dsonar.organization=sagarinfotech -Dsonar.projectKey=credit-service-sagarb'		
    		}
  }

}
node('kubernetes'){
   container('podman') {
	stage('Image Build'){
	   unstash 'myproject'
	   sh 'podman image build -t credit-service .'	
		
	}
   }
}
}
