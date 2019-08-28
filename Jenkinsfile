pipeline {
    agent { docker { image 'python:3.7.4' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
                sh 'echo "Hello World!"'
                sh '''
                    echo "Multiline shell steps work too!"
                    ls -lah
                '''
                pip install Flask
            }
        }
    }
}
