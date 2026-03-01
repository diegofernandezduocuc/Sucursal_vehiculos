pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Git Clone') {
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
                sh 'sudo docker build -t imagen_vehiculos .'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sudo docker stop contenedor_sucursal || true'
                sh 'sudo docker rm contenedor_sucursal || true'
                sh 'sudo docker run -d -p 9090:8080 --name contenedor_sucursal imagen_vehiculos'
            }
        }
    }
}