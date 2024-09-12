pipeline {
    agent any

    environment {
        // Define environment variables for Python
        VENV = 'venv' // Virtual environment directory
        // REQUIREMENTS = 'requirements.txt' // Requirements file for dependencies
        DJANGO_SETTINGS_MODULE = 'django_demo.settings' // Replace with your Django project name
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                git branch: 'main', url: 'https://github.com/okechpj/django-jenkins-demo.git'
            }
        }

        
        stage('Setup Python Environment') {
            steps {
                script {
                    // Setup virtual environment
                    sh 'python3 -m venv ${VENV}'
                    sh './${VENV}/bin/pip install --upgrade pip'
                }
            }
        }

        // stage('Install Dependencies') {
        //     steps {
        //         script {
        //             // Install Django and other dependencies
        //             sh './${VENV}/bin/pip install -r ${REQUIREMENTS}'
        //         }
        //     }
        // }

        stage('Run Migrations') {
            steps {
                script {
                    // Apply database migrations
                    sh './${VENV}/bin/python3 manage.py migrate'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run Django tests
                    sh './${VENV}/bin/python3 manage.py test'
                }
            }
        }

        stage('Static Analysis') {
            steps {
                script {
                    // Run code quality checks (e.g., flake8)
                    sh './${VENV}/bin/flake8 .'
                }
            }
        }

        stage('Package Application') {
            steps {
                script {
                    // Package the application (e.g., create a Docker image if needed)
                    sh 'echo "Packaging step"'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy the application (this step can be customized as needed)
                    sh 'echo "Deploy step"'
                }
            }
        }
    }

    post {
        always {
            // Cleanup virtual environment
            script {
                sh 'rm -rf ${VENV}'
            }
        }
        success {
            echo 'Build and deployment completed successfully!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
