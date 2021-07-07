node {
   def customImage

    stage('Clone repository') {
     
        checkout scm
    }

    stage('Build image') {
  
    customImage = docker.build("my-image:${env.BUILD_ID}")
	customImage.inside {
		sh 'npm test'
    }
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'git') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

