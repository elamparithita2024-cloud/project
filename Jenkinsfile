pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT', 
            choices: ['dev', 'staging', 'prod'], 
            description: 'Select the deployment target environment'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
            }
        }

        stage('Build') {
            steps {
                echo "Performing compile check on app.py..."
                // Properly escaped parentheses using carets (^) for Windows Batch
                bat '''
                    if not exist app.py echo print^("Testing pipeline execution"^) > app.py
                    python -m py_compile app.py
                '''
            }
        }

        stage('Deploy') {
            steps {
                input message: "Approve deployment to ${params.ENVIRONMENT}?", ok: "Go"
                
                echo "Deploying to ${params.ENVIRONMENT}..."
                bat 'python app.py'
            }
        }
    }
}
