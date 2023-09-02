pipeline {
    agent {
        docker {
            image 'bridgecrew/checkov:latest'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/chndel-abhishek/Notejam-Jenkins.git']]])
                script { 
                    sh """pip install pipenv
                    pipenv run pip install bridgecrew
                    pipenv run bridgecrew --directory . --bc-api-key 0eae2fff-00a2-46e6-8cff-8fc1a1522150 --repo-id chndel-abhishek/Notejam-Jenkins"""
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}
