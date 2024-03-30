pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'commande_unix'
                    } else {
                        bat 'start commande_windows'
                    }
                }
            }
        }
    }
}
