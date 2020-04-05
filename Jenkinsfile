node('slave1'){
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'docker.io/ankushgupta0727/docker-test'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/ankushgupta/node-todo-frontend'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
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
