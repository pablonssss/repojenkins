pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clono el repo desde GitHub
                git 'https://github.com/pablonssss/repojenkins.git'
            }
        }

        stage('Verifico si el apache esta instalado') {
            steps {
                // Verifica si Apache está instalado en la VM2
                sshagent(['55c5edfe-cded-4a87-937b-b381846887a3']) {
                    sh 'ssh -o StrictHostKeyChecking=no pablo@10.0.2.17 "sudo systemctl status apache2 || sudo apt-get install apache2 -y"'
                }
            }
        }

        stage('Configure Apache') {
            steps {
                // Configura Apache en la VM2
                sshagent(['55c5edfe-cded-4a87-937b-b381846887a3']) {
                    sh 'ssh pablo@10.0.2.17 "sudo systemctl start apache2 && sudo systemctl enable apache2"'
                }
            }
        }

        stage('Deploy Apache') {
            steps {
                // Copia el archivo index.html al directorio de Apache en la VM2
                sshagent(['55c5edfe-cded-4a87-937b-b381846887a3']) {
                    sh 'scp index.html pablo@10.0.2.17:/var/www/html/index.html'
                }
            }
        }
    }

    post {
        success {
            echo 'Despliegue completado con éxito en Apache (VM2).'
        }
        failure {
            echo 'El pipeline ha fallado. Verifica los logs para más detalles.'
        }
    }
}

