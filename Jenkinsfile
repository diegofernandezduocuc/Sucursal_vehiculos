pipeline {
    agent any

    tools {
        maven 'M3'
    }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-amazon-corretto'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clon de Git') {
            steps {
                git branch: 'main', url: 'https://github.com/diegofernandezduocuc/Sucursal_vehiculos.git'
            }
        }

        stage('Build Application - Maven') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Docker Image') {
            steps {
                sh 'docker build -t imagen_vehiculos .'
            }
        }

        stage('Deployment') {
            steps {
                sh 'docker stop contenedor_sucursal || true'
                sh 'docker rm contenedor_sucursal || true'
                sh 'docker run -d -p 9090:8080 --name contenedor_sucursal imagen_vehiculos'
            }
        }
    }
}