pipeline {
    agent any

    environment {
        TF_VERSION = "1.5.6"  // Specify your Terraform version
        TF_PATH = "/usr/local/bin/terraform"  // Path to Terraform binary
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Initialize Terraform') {
            steps {
                sh "${TF_PATH} init"
            }
        }
        stage('Validate Terraform') {
            steps {
                sh "${TF_PATH} validate"
            }
        }
        stage('Plan Terraform') {
            steps {
                sh "${TF_PATH} plan -out=tfplan"
            }
        }
        stage('Apply Terraform') {
            steps {
                input message: "Approve to apply Terraform changes?", ok: "Apply"
                sh "${TF_PATH} apply tfplan"
            }
        }
    }
    post {
        always {
            cleanWs() // Clean workspace after the build
        }
    }
}
