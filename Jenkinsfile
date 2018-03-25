pipeline {
    agent {
        docker {
            image 'alpine:latest'
            args '-v /tmp:/tmp'
        }
    }
    stages {
        stage('Pipeline Setup') {
            steps {
                echo 'Pipeline Essential - Fetch Scripts'
                sh 'apk add --update alpine-sdk bash php7'
                sh 'ls -al /tmp/'
                sh 'php -m | tee -a /tmp/php-modules.txt'
                sh 'ls -al /tmp/'
            }
        }
        stage('DB Export') {
            steps {
                echo 'MySQL/MariaDB Instance - Data Export'
                sh 'apk add --update mariadb-client'
                sh 'ls -al ./'
                sh './db-setup-cnf.sh'
                sh 'cp ./my.cnf ~/.my.cnf'
                sh 'cat ~/.my.cnf'
                sh 'mysqldump --print-defaults'
                sh 'mysqldump --databases db_wesites_dev > /tmp/db-wesites-dev.sql'
                sh 'ls -al /tmp/'
            }
        }
    }
}
