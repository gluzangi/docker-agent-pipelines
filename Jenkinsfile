pipeline {
    agent {
        docker {
            image 'php:cli'
            args '-v /tmp:/tmp'
        }
    }
    stages {
        stage(Build) {
            steps {
                sh 'printenv'
                sh 'php -m'
            }
        }
    }
}
