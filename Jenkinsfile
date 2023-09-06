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
                    sh """pipenv install
                    pipenv run pip install bridgecrew
                    pipenv run bridgecrew --directory . --bc-api-key 8baca0d4-422d-46d8-adca-5564629fe581 --repo-id chndel-abhishek/Notejam-Jenkins"""
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}
