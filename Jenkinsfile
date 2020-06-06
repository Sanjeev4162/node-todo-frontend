node('slave1'){
    
	

    env.AWS_ECR_LOGIN=true
    def npmHome
    def newApp
    def registry = env.registry
    def registryCredential =  env.registryCredential
	
	stage('Git') {
		npmHome = tool 'node'
		git 'https://github.com/ankushgupta/node-todo-frontend'
	}
	stage('Build') {
		sh '/home/jenkins/tools/jenkins.plugins.nodejs.tools.NodeJSInstallation/node/bin/npm install'
	}
	stage('Test') {
		sh '/home/jenkins/tools/jenkins.plugins.nodejs.tools.NodeJSInstallation/node/bin/npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			//newApp.push()
        }
	}
	stage('Registring image') {
        //docker.withRegistry( 'https://' + registry, registryCredential ) {
    	//	newApp.push 'latest2'
		sh "docker push docker.io/ankushgupta0727/docker-test:$BUILD_NUMBER"
       // }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        //sh "docker rmi $registry:latest"
    }
    
}
