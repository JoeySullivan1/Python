pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Limpiar Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Clonar Repositorio') {
            steps {
                checkout scm
            }
        }
        stage('Instalar Dependencias') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-venv
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install pytest
                '''
            }
        }
        stage('Ejecutar Pruebas') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest test.py
                '''
            }
        }
    }
    post {
        always {
            echo 'Pipeline completado'
        }
        success {
            echo 'El pipeline fue exitoso'
        }
        failure {
            echo 'El pipeline falló'
        }
    }
}
