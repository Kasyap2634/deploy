
pipeline {
    agent none

    stages {

        stage('build') {
            agent {
                label 'buildnode'
            }

            steps {
                deleteDir()

                sh """
                    git clone https://github.com/Kasyap2634/deploy.git
                    ls -la
                """

                stash name: 'webpage',
                      includes: 'deploy/**'
            }
        }

        stage('deploy') {
            agent {
                label 'deploynode'
            }

            steps {
                deleteDir()

                unstash 'webpage'

                sh """
                    sudo rm -rf /var/www/html/*
                    sudo cp -r deploy/* /var/www/html/
                    ls -la /var/www/html/
                """
            }
        }
    }
}
