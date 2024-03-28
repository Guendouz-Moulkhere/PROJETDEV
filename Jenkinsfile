pipeline {
    agent any
    
    stages {
        stage('Example') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'commande_unix'
                    } else {
                        bat 'commande_windows'
                    }
                }
            }
        }
    }
}
