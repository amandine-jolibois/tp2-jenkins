pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Récupère ton code depuis Git
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                // Installe les dépendances Python
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run tests') {
            steps {
                // Lance pytest
                sh 'pytest --maxfail=1 --disable-warnings -q'
            }
        }
    }

    post {
        success {
            echo "✅ Build réussi, tous les tests sont passés !"
        }
        failure {
            echo "❌ Échec du build, au moins un test a échoué."
        }
    }
}
