pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from repo
                checkout scm
            }
        }

        stage('Prepare') {
            steps {
                script {
                    // Clean old dist folder and create a new one
                    if (isUnix()) {
                        sh '''
                        rm -rf dist
                        mkdir dist
                        cp *.html dist/
                        cp -r css dist/
                        cp -r js dist/
                        cp -r images dist/
                        '''
                    } else {
                        bat '''
                        if exist dist rmdir /s /q dist
                        mkdir dist
                        xcopy *.html dist\\ /Y
                        xcopy css dist\\css\\ /E /Y
                        xcopy js dist\\js\\ /E /Y
                        xcopy images dist\\images\\ /E /Y
                        '''
                    }
                }
            }
        }

        stage('Validate') {
            steps {
                echo "Run HTML/CSS/JS validation here if needed"
            }
        }
    }

    post {
        always {
            // Save artifacts for later download
            archiveArtifacts artifacts: 'dist/**', allowEmptyArchive: false
        }
    }
}
