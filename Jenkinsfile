pipeline {
    agent any

    tools {
        nodejs 'nodejs.10' // Ensure this matches the exact name of your NodeJS tool configuration in Jenkins
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Clone the repository from your version control system
                git branch: 'main', url: 'https://github.com/jaiswaladi246/demo_nodejs_webpage.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install dependencies
                sh 'npm install'
            }
        }
        
        // Uncomment and configure this stage if OWASP Dependency Check is needed
        // stage("OWASP Dependency Check") {
        //     steps {
        //         dependencyCheck additionalArguments: '--scan ./ --format HTML', odcInstallation: 'DP'
        //         dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
        //     }
        // }
        
        stage('Docker build and push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'ba705d80-36e5-44ca-ac03-e5e66d08c970', toolName: 'docker') {
                        // Build the Docker image
                        sh 'docker build -t demonodejs .'
                        // Tag the Docker image
                        sh 'docker tag demonodejs simonkolz/nodejs:latest'
                        // Push the Docker image to Docker Hub
                        sh 'docker push simonkolz/nodejs:latest'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                // Run the tests
                sh 'echo test'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application
                sh 'echo deploy'
            }
        }
    }
}
