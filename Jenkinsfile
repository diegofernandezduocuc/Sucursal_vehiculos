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
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Image') {
            steps {
                bat 'docker build -t imagen_vehiculos .'
            }
        }

        stage('Deployment') {
            steps {
                bat 'docker stop contenedor_sucursal || exit 0'
                bat 'docker rm contenedor_sucursal || exit 0'
                bat 'docker run -d -p 9090:8080 --name contenedor_sucursal imagen_vehiculos'
            }
        }
    }
}