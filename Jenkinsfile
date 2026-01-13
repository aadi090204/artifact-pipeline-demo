pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'fetching source code'
                checkout scm
            }
        }

        stage('Code Quality Check!') {
            steps {
                echo 'Checking code quality'
                bat '''
                findstr GOOD quality.txt > nul
                if errorlevel 1 (
                    echo Code quality failed
                    exit 1
                ) else (
                    echo code quality passed
                )
                '''
            }
        }

        stage('Generate Report') {
            steps {
                echo 'Generating build report'
                bat '''
                mkdir reports
                echo Build Successful > reports\\build-report.txt
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving reports'
                archiveArtifacts artifacts: 'reports/*.txt', fingerprint: true
            }
        }

    }

    post {
        success {
            echo 'pipeline completed successfully'
        }
        failure {
            echo 'pipeline failed - code blocked'
        }
    }
}
