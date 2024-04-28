pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/VelpulaAkkini/fastapijenkTOimage.git']]])
            }
        }
        
        stage('Build image') {
            steps {
                def app = docker.build("nagvelpula/test")
            }
        }
        
        stage('Test image') {
            steps {
                app.inside {
                    sh 'echo "Tests passed"'
                }
            }
        }
        
        stage('Push image') {
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'nagvelpula/******') {
                    app.push("${env.BUILD_NUMBER}")
                }
            }
        }
        
        stage('Trigger ManifestUpdate') {
            steps {
                echo "Triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
            }
        }
    }
}
