pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build/Prepare') {
            steps {
                bat """
                if exist dist rmdir /s /q dist
                mkdir dist
                xcopy home.html dist\\ /Y
                xcopy about.html dist\\ /Y
                xcopy contact.html dist\\ /Y
                xcopy explore.html dist\\ /Y
                xcopy customize.html dist\\ /Y
                xcopy packages.html dist\\ /Y
                xcopy travelguide.html dist\\ /Y
                xcopy itinerary.html dist\\ /Y
                xcopy moon.html dist\\ /Y
                xcopy css dist\\css\\ /E /Y
                xcopy js dist\\js\\ /E /Y
                xcopy images dist\\images\\ /E /Y
                """
            }
        }

        stage('Validate') {
            steps {
                echo "You could add HTML/CSS linting here"
            }
        }

        stage('Run (Preview)') {
            steps {
                echo "Static website doesn’t run like Java, but you can serve dist/home.html"
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dist/**', allowEmptyArchive: false
        }
    }
}
