pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocatedr
        timeout(time: 1, unit: 'SECONDS')
    }
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
