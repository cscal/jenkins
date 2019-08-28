pipeline {
    agent { docker { image 'python' } }
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
