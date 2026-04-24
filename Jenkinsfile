pipeline {
    agent any

    stages {
        stage('Info'){
            steps {
                echo "Gałąź: ${env.GIT_BRANCH}"
                echo "Build: ${env.BUILD_NUMBER}"

            }
        }
        stage('Testy'){
            steps{
                echo "Uruchomienie testów"
                sh 'python3 test_app.py'
            }
        }
        stage('Build'){
            steps{
                echo "Budowanie"
                sh 'docker build -t nazwa_obrazu .'
            }
        }
        stage('Deploy'){
            steps{
                echo "Deployowanie"
                sh 'docker stop moj_kontener'
                sh 'docker run -d -p 5000:5000 --name moj_kontener nazwa_obrazu'
            }
        }
    }
    post {
        success {
            echo "OK"
        }
        failure {
            echo "BLAD! Sprawdź logi!"
        }
    }
}