pipeline {
    agent any
    environment {
        // Configuración de variables de entorno
        EMAIL_RECIPIENTS = 'team@example.com'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Clonando repositorio...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Compilando el proyecto...'
                sh 'mvn clean install' // Usa el comando de compilación apropiado para tu proyecto
            }
        }
        stage('Test') {
            steps {
                echo 'Ejecutando pruebas...'
                sh 'mvn test' // Reemplaza con las pruebas específicas de tu proyecto
            }
        }
        stage('Deploy') {
            steps {
                echo 'Desplegando a entorno de pruebas...'
                sh './deploy.sh' // Simula el despliegue con un script de ejemplo
            }
        }
    }
    post {
        success {
            echo 'Pipeline ejecutado con éxito.'
            mail to: "${EMAIL_RECIPIENTS}",
                 subject: "Éxito: Build ${env.BUILD_NUMBER}",
                 body: "El pipeline fue ejecutado correctamente. Revisión ${env.GIT_COMMIT}."
        }
        failure {
            echo 'Pipeline falló.'
            mail to: "${EMAIL_RECIPIENTS}",
                 subject: "Fallo: Build ${env.BUILD_NUMBER}",
                 body: "El pipeline falló. Por favor revisa los logs."
        }
    }
}

