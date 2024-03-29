pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    try {
                        sh 'mvn clean package'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    try {
                        sh 'mvn test'
                        junit '**/target/surefire-reports/*.xml' // Capture des rapports de test
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // Ajoutez ici les étapes de déploiement de votre application
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true // Archiver les artefacts de build
            junit '**/target/surefire-reports/*.xml' // Archiver les rapports de test
        }
        success {
            emailext (
                subject: "Build réussi: ${currentBuild.fullDisplayName}",
                body: "Le build ${currentBuild.fullDisplayName} a réussi.",
                recipientProviders: [culprits(), developers()]
            )
        }
        failure {
            emailext (
                subject: "Échec du build: ${currentBuild.fullDisplayName}",
                body: "Le build ${currentBuild.fullDisplayName} a échoué. Veuillez vérifier les logs pour plus d'informations.",
                recipientProviders: [culprits(), developers()]
            )
        }
    }
}
