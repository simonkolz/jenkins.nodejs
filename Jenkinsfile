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
                    withDockerRegistry(credentialsId: '8491bc31-eedd-4abc-a070-d0c0e0aec1c5', toolName: 'Docker') {
                        // Build the Docker image
                        sh 'docker build -t demonodejs .'
                        // Tag the Docker image
                        sh 'docker tag demonodejs:latest simonkolz/docker-node.js:1.0'
                        // Push the Docker image to Docker Hub
                        sh 'docker push simonkolz/docker-node.js:1.0'
                    }
                }
            }
        }
        
        stage('Docker run') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '8491bc31-eedd-4abc-a070-d0c0e0aec1c5', toolName: 'Docker') {
                        sh 'docker run -d --name demo-nodejs -p 8081:8081 simonkolz/docker-node.js:1.0'
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
