pipeline {
    agent { docker { image 'python:3.7.4' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
                sh 'pip install Flask'
                sh 'flask --version'
                sh 'echo "Hello World!"'
                sh '''
                    echo "Multiline shell steps work too!"
                    ls -lah
                '''
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
    }
}
