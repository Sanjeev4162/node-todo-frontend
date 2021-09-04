node('slave1'){    

	
	stage('Git') {
		npmHome = tool 'nodejs16'
		git 'https://github.com/ankushgupta/node-todo-frontend'
	}
	stage('Build') {
  		 sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
       // docker.withRegistry( 'https://' + registry, registryCredential ) {
	 ////	    def buildName = registry + ":$BUILD_NUMBER"
	////		newApp = docker.build buildName
			//newApp.push()
		sh "docker build -t docker-test:$BUILD_NUMBER ."
		sh "docker tag docker-test:$BUILD_NUMBER ankushgupta0727/docker-test:$BUILD_NUMBER"
        ////}
	}
	stage('Registring image') {
        //docker.withRegistry( 'https://' + registry, registryCredential ) {
    	//	newApp.push 'latest2'
		withCredentials([usernamePassword(credentialsId: 'registryCredential', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
               sh "docker login -u=$USER -p=$PASS"
               sh "echo ankushgupta0727/docker-test:$BUILD_NUMBER "
		sh "docker push ankushgupta0727/docker-test:$BUILD_NUMBER"
        }
	}
    stage('Removing image') {
        sh "docker rmi ankushgupta0727/docker-test:$BUILD_NUMBER"
        //sh "docker rmi $registry:latest"
    }
    
}
