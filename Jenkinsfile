pipeline {
    agent { node { label 'Agent -1'}}


    stages {
        stage('Build') {
            steps {
                echo 'Building....'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing....'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }

    post {
        always {
            echo 'I will always run weather job is success or not'
        },
        success{
            echo 'I will run only when job is success'
            
        }

        failure{
            echo 'I will run when failure'
        }

    }
}