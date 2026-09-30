pipeline {
    agent any

    options {
        disableConcurrentBuilds()
    }

    stages {
        stage('Check website') {
            steps {
                sh 'test -s index.html'
            }
        }

        stage('Deploy website') {
            steps {
                sh '''
                    install -m 644 index.html /var/www/jenkins-site/index.html.new
                    mv -f /var/www/jenkins-site/index.html.new /var/www/jenkins-site/index.html
                '''
            }
        }

        stage('Verify website') {
            steps {
                sh '''
                    curl -fsS http://127.0.0.1/ -o served.html
                    cmp index.html served.html
                '''
            }
        }
    }
}
