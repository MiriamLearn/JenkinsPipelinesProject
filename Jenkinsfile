pipeline {
    agent any

    parameters {
        string(name: 'REPO_URL',defaultValue: 'https://github.com/MiriamLearn/JenkinsPipelinesProject', description: 'GitHub repository URL')
        string(name: 'NAME_BRANCH', defaultValue: 'main', description: 'Branch name to build')
    }

    environment {
        MAIN_BRANCH = 'main' // שם הבראנצ' המרכזי להגדרה בסיסית
    }

    triggers {
        cron('30 5 * * 1') // ימי שני 05:30
        cron('0 14 * * *') // כל יום 14:00
    }

    stages {

        stage('Checkout Code') {
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
            timeout(time: 5, unit: 'MINUTES')
        }

        stage('Compile') {
            steps {
                echo "Starting compilation stage"
                sh 'mvn compile'
                echo "Compilation stage completed successfully"
            }
            timeout(time: 5, unit: 'MINUTES')
        }

        stage('Run Tests') {
            steps {
                echo "Starting test stage"
                sh 'mvn test'
                echo "Test stage completed successfully"
            }
            timeout(time: 5, unit: 'MINUTES')
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
