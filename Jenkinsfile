pipeline {
    agent any

    environment {
        TEST_ENV = 'C:\\EntornoPruebas'
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
                dir('subdirectorio-del-pom') { // Ajusta si el pom.xml está en un subdirectorio
                    bat 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando pruebas...'
                dir('subdirectorio-del-pom') { // Ajusta según sea necesario
                    bat 'mvn test'
                }
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
            mail to: 'tuemail@ejemplo.com',
                 subject: "Pipeline Exitoso: ${currentBuild.fullDisplayName}",
                 body: "El pipeline fue ejecutado exitosamente.\nRevisar detalles aquí: ${env.BUILD_URL}"
        }
        failure {
            echo 'Pipeline falló.'
            mail to: 'tuemail@ejemplo.com',
                 subject: "Pipeline Fallido: ${currentBuild.fullDisplayName}",
                 body: "El pipeline falló en la etapa ${env.STAGE_NAME}.\nRevisar detalles aquí: ${env.BUILD_URL}"
        }
    }
}
