pipeline {
    agent any // Se ejecuta en cualquier agente disponible

    stages {
        stage('Preparación') {
            steps {
                // Comando para asegurar que se usa Python
                sh 'python --version'
                // Instalar dependencias
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Ejecución de Regresión Visual') {
            steps {
                // Ejecuta el script de Python
                // Importante: Si tu script necesita alguna configuración o 
                // ambiente específico (como un navegador para Selenium), 
                // asegúrate de que esté disponible en el agente de Jenkins.
                sh 'python regre_visual_tn_prod.py'
            }
        }
        stage('Post-Ejecución') {
            steps {
                // Aquí puedes añadir pasos para publicar reportes, enviar notificaciones, etc.
                echo 'Script de regresión visual finalizado.'
            }
        }
    }
}
