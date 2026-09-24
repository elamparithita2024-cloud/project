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
                
                // Native Groovy step to safely create a perfectly formatted Python file
                writeFile file: 'app.py', text: 'print("Testing pipeline execution")\n'
                
                // Run the compilation check
                bat 'python -m py_compile app.py'
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
