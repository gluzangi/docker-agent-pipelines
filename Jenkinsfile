pipeline {
    agent {
        docker {
            image 'php:cli'
            args '-v /tmp:/tmp'
        }
    }
    stages {
        stage('Pipeline Setup') {
            steps {
                sh 'ls -al /tmp/'
                sh 'php -m | tee -a /tmp/php-modules.txt'
                sh 'ls -al /tmp/'
            }
        }
        stage('DB Export') {
            agent { 
                docker {
                    image 'mariadb:latest'
                    /*args '-v /tmp:/tmp'*/
                }
            }
            steps {
                echo 'MySQL/MariaDB Instance - Data Export'
                sh 'ls -al ./'
                sh './db-setup-cnf.sh'
                sh 'cp ./my.cnf ~/.my.cnf'
                sh 'cat ~/.my.cnf'
                sh 'mysqldump --print-defaults'
                sh 'mysqldump --databases db_wesites_dev > db-wesites-dev.sql'
                sh 'ls -al ./'
            }
        }
    }
}
