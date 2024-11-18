pipeline {
    agent any

    environment {
        TEST_ENV = 'C:\\EntornoPruebas' // Ruta al entorno de pruebas en Windows
    }

    tools {
        maven 'Maven 3.9.9'
        jdk 'JDK 17'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Clonando el repositorio...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilando el proyecto...'
                bat 'mvn clean install' // Comando para Windows
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando pruebas...'
                bat 'mvn test'
            }
        }

        stage('Deploy to Test Environment') {
            steps {
                echo 'Desplegando en el entorno de pruebas...'
                bat """
                copy target\\*.jar ${TEST_ENV}
                echo 'Despliegue completado.'
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline ejecutado exitosamente.'
            mail to: 'j.p25gb@gmail.com',
                 subject: "Pipeline Exitoso: ${currentBuild.fullDisplayName}",
                 body: "El pipeline fue ejecutado exitosamente.\nRevisar detalles aquí: ${env.BUILD_URL}"
        }
        failure {
            echo 'Pipeline falló.'
            mail to: 'j.p25gb@gmail.com',
                 subject: "Pipeline Fallido: ${currentBuild.fullDisplayName}",
                 body: "El pipeline falló en la etapa ${env.STAGE_NAME}.\nRevisar detalles aquí: ${env.BUILD_URL}"
        }
    }
}
