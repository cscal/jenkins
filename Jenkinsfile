pipeline {
    agent { docker { image 'python:3.7.4' } }
    stages {
        stage('Build') {
            steps {
                sh 'python --version'
                sh 'pip install Flask'
                sh 'flask --version'
                sh 'git clone https://github.com/pallets/flask'
                sh 'pip install -e flask/examples/tutorial'
            }
        }
        stage('Test') {
            steps {
                sh 'pip install flask/examples/tutorial/.[test]'
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
            echo 'Complete and total failure'
        }
        unstable {
            echo 'Something in the code is not passing tests'
        }
    }
}
