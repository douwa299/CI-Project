pipeline {
    agent any

    environment {
        PATH = "C:\\Users\\tech\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\tech\\AppData\\Local\\Programs\\Python\\Python313\\Scripts;${env.PATH}"
    }

    stages {
        stage('Clonage') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/douwa299/CI-Project.git'
            }
        }
        stage('Vérification Python') {
            steps {
                bat 'python --version'
                bat 'python -m pip --version'
            }
        }
        stage('Installation des dépendances') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }
        stage('Analyse qualité code - Pylint') {
            steps {
                // make the build fail if the score is below 8
                bat 'python -m pylint calculator.py || exit /b 0'
                bat 'python -m pylint calculator.py'
            }
        }
        stage('Tests unitaires') {
            steps {
                bat 'python -m pytest'
            }
        }
    }
    post {
        always  { echo 'Pipeline terminé' }
        success { echo 'BUILD SUCCESS' }
        failure { echo 'BUILD FAILED' }
    }
}