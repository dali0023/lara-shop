pipeline {
    agent any
    stages {
        stage("Verify tooling") {
            steps {
                sh '''
                    docker info
                    docker version
                    docker compose version
                '''
            }
        }        
        stage("Clear all running docker containers") {
            steps {
                script {
                    try {
                        sh 'docker rm -f $(docker ps -a -q)'
                    } catch (Exception e) {
                        echo 'No running container to clear up...'
                    }
                }
            }
        }
        stage("Start Docker") {
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
                // sh 'make up'
            }
        }
        stage("Run Composer Install") {
            steps {
                sh 'docker compose run --rm composer install'
                // sh 'composer install'
            }
        }            
        // stage("Run Tests") {
        //     steps {
        //         sh 'docker compose run --rm artisan test'
        //         sh "docker compose run --rm ./vendor/bin/phpunit"
        //     }
        // }
    }
    // post {       
    //     always {
    //         sh 'docker compose down --remove-orphans -v'
    //         sh 'docker compose ps'
    //     }
    // }
}