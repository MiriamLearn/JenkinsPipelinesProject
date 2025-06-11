pipeline {
    agent any

    parameters {
        string(name: 'REPO_URL', defaultValue: 'https://github.com/MiriamLearn/JenkinsPipelinesProject', description: 'GitHub repository URL')
        string(name: 'NAME_BRANCH', defaultValue: 'main', description: 'Branch name to build')
    }

    environment {
        MAIN_BRANCH = 'main' // שם הבראנצ' המרכזי להגדרה בסיסית
    }

    triggers {
        cron('30 5 * * 1') // לדוגמה: ימי שני 05:30
    }

    stages {

        stage('Checkout Code') {
            options {
                timeout(time: 5, unit: 'MINUTES')
            }
            steps {
                script {
                    echo "Starting checkout stage"

                    if (params.NAME_BRANCH == env.MAIN_BRANCH) {
                        checkout scm
                    } else {
                        git branch: "${params.NAME_BRANCH}", url: "${params.REPO_URL}"
                    }

                    echo "Checkout stage completed successfully"
                }
            }
        }

        stage('Compile') {
            options {
                timeout(time: 5, unit: 'MINUTES')
            }
            steps {
                echo "Starting compilation stage"
                sh 'mvn compile'
                echo "Compilation stage completed successfully"
            }
        }

        stage('Run Tests') {
            options {
                timeout(time: 5, unit: 'MINUTES')
            }
            steps {
                echo "Starting test stage"
                sh 'mvn test'
                echo "Test stage completed successfully"
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully 🎉"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}

