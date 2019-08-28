pipeline {
    agent { docker { image 'python:3.7.4' } }
    stages {
        stage('Build') {
            steps {
                sh 'python --version'
                sh 'pip install Flask'
                sh 'flask --version'
                sh 'git clone https://github.com/pallets/flask'
                sh 'cd flask/examples/tutorial'
                sh 'pip install -e .'
            }
        }
        stage('Test') {
            steps {
                sh 'pip install ".[test]"'
                sh 'pytest'
                sh 'coverage run -m pytest'
                sh 'coverage report'
                sh 'coverage html'
            }
        }
    }
    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        failure {
            mail to: 'calhoun.charlie@gmail.com',
                subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Something is wrong with ${env.BUILD_URL}"
        }
        unstable {
            mail to: 'calhoun.charlie@gmail.com',
                subject: "Unstable Pipeline: ${currentBuild.fullDisplayName}",
                body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
}
