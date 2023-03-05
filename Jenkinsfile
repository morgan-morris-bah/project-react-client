node {
    stage ("Checkout React Client"){
        git branch: 'main', url: 'https://github.com/morgan-morris-bah/project-react-client.git'
    }
    
    stage ("NPM Install") {
        sh 'npm install'
    }

    stage ("Containerize the app-docker build - React") {
        sh 'docker build --rm -t react:v1.0 .'
    }
    
    stage ("Inspect the docker image - React"){
        sh "docker images react:v1.0"
        sh "docker inspect react:v1.0"
    }
    
    stage ("Run Docker container instance - React"){
        sh "docker run -d --rm --name react -p 3000:80 react:v1.0"
     }
 
    stage('User Acceptance Test - React') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {
	  
	    stage('Release - AuthService') {
	      sh 'docker stop react'
	      sh 'echo MCC AuthService is ready to release!'
	    }
	  }
    }
}
