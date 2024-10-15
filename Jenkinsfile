pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio desde GitHub
                git branch: 'main', url: 'https://github.com/pablonssss/repojenkins.git'
            }
        }

        stage('Verifico si Apache está instalado') {
            steps {
                // Verificar si Apache está instalado en VM2, instalar si es necesario
                sshagent(['1092453d-8fad-4168-9714-ba0d89b5773c']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no pablo@10.0.2.17 "
                        if ! systemctl is-active --quiet apache2; then
                            sudo apt-get update
                            sudo apt-get install apache2 -y
                        fi"
                    '''
                }
            }
        }

        stage('Configurar Apache') {
            steps {
                // Configurar y habilitar Apache en la VM2
                sshagent(['1092453d-8fad-4168-9714-ba0d89b5773c']) {
                    sh 'ssh pablo@10.0.2.17 "sudo systemctl is-active --quiet apache2 || sudo systemctl start apache2 && sudo systemctl enable apache2"'
                }
            }
        }

        stage('Deploy en Apache') {
            steps {
                // Copiar el archivo index.html al servidor Apache en VM2
                sshagent(['1092453d-8fad-4168-9714-ba0d89b5773c']) {
                    sh 'scp -o StrictHostKeyChecking=no index.html pablo@10.0.2.17:/var/www/html/index.html'
                }
            }
        }
    }

    post {
        success {
            // Mensaje en caso de éxito
            echo 'Despliegue completado con éxito en Apache (VM2).'
        }
        failure {
            // Mensaje en caso de fallo
            echo 'El pipeline ha fallado. Verifica los logs para más detalles.'
        }
    }
}
