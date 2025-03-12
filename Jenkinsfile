pipeline {
    agent any

    environment {
        APP_NAME = 'proyecto-jenkins'
        DEPLOY_ENV = 'staging'
        GIT_REPO = 'https://github.com/Aiza0102/proyecto-jenkins.git'
        BUILD_DIR = 'build'
    }

    stages {
        stage('Checkout') {
            steps {
                git GIT_REPO
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        echo "Compilando la aplicación ${APP_NAME}..."
                        sh 'mkdir -p ${BUILD_DIR} && echo "Archivo de prueba" > ${BUILD_DIR}/app.txt'
                        echo "Compilación completada exitosamente."
                    } catch (Exception e) {
                        echo "Error en la compilación: ${e.getMessage()}"
                        error("Fallo en la etapa de compilación")
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo "Ejecutando pruebas en entorno ${DEPLOY_ENV}..."
                    sh 'echo "Pruebas ejecutadas correctamente"'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    echo "Empaquetando archivos para despliegue..."
                    sh 'tar -czf ${BUILD_DIR}/package.tar.gz ${BUILD_DIR}/app.txt'
                }
            }
        }

        stage('Deploy Simulation') {
            steps {
                script {
                    echo "Desplegando aplicación ${APP_NAME} en entorno ${DEPLOY_ENV}..."
                    sh 'mv ${BUILD_DIR}/package.tar.gz /tmp/'
                }
            }
        }
    }
}