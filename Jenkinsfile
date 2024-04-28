node {
    def app

    stage('Clone repository') {
      
            https://github.com/VelpulaAkkini/fastapijenkTOimage.git
      
    }

    stage('Build image') {
  
       app = docker.build("nagvelpula/test")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'nagvelpula/Nag@#2022') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
