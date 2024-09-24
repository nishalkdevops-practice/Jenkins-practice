pipeline {
    agent { node { label 'Agent-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    }

    // triggers {
    //     cron('* * * * *')
    // }


    environment {
        USER = 'Nishal'
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }




    stages {
        stage('Build') {
            steps {
                echo 'Building..........'
                sh '''
                    ls -ltr
                    pwd
                    echo 'this is to test the github webhook events if any changes happen in github automatically pipeline will trigger'
                    printenv

                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing.......'
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Unit Testing....'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
                //error 'this is failed'
            }
        }

        stage('Validation') {
            environment {
                AUTH = credentials('ssh-auth')
            }

            steps {
                sh 'printenv'
            }

        }

        stage('Example') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        }

        stage('Approval') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "Nishal"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
        
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }

        stage('Prod deploy') {
            when {
                 environment name: 'USER', value: 'Nishal'
            }
            steps {
                echo 'deploying to the prod'
            }
        }

        stage('Parallel Stage') {
 
            parallel {
                stage('Branch A') {
                    steps {
                        echo "On Branch A"
                        sh 'sleep 10'
                    }
                }
                stage('Branch B') {
                    steps {
                        echo "On Branch B"
                        sh 'sleep 10'
                    }
                }
                stage('Branch C') {
                    stages {
                        stage('Nested 1') {
                            steps {
                                echo "In stage Nested 1 within Branch C"
                                sh 'sleep 10'
                            }
                        }

                    }
                }
            }
        }
    }

    post {
        always {
            echo 'I will always run weather job is success or not'
        }

        success{
            echo 'I will run only when job is success'
            
        }

        failure{
            echo 'I will run when failure'
        }

    }
}
