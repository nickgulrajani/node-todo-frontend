pipeline {
    
        environment {
        registry = "nicholasgull/nodefrontend"
        registryCredential = 'dockerhub'
        dockerImage = ''	
        }
	agent any 
        stages {
	stage('Git') {
        steps
        {
		git 'https://github.com/nickgulrajani/node-todo-frontend'
	}
        }
	stage('Build') {
        steps
        {

		sh 'npm install'
	}
        }
	stage('Test') {
        steps
        {

		sh 'npm test'
        }
	}
	stage('Building image') {
        steps
        {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
        }
	}
	stage('Registring image') {
        steps
        {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
        }
    stage('Removing image') {
      steps
       {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
}
}
