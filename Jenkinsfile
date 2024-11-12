pipeline {
    agent any
    parameters {
        string(name: 'maven_version', defaultValue: '3.9.3', description: 'Pass the version of Maven')
        string(name: 'terraform_version', defaultValue: '1.8.5', description: 'Pass the version of Terraform')
    }
    stages {
        stage('Download Maven') {
            steps {
                script {
                    // Ensure the maven_version parameter is not empty
                    if (!params.maven_version) {
                        error "Maven version parameter is missing!"
                    }
                }
                sh '''
                cd /var/lib/jenkins/
                sudo wget https://dlcdn.apache.org/maven/maven-3/${maven_version}/binaries/apache-maven-${maven_version}-bin.tar.gz
                '''
            }
        }
        stage('Download Terraform') {
            steps {
                script {
                    // Ensure the terraform_version parameter is not empty
                    if (!params.terraform_version) {
                        error "Terraform version parameter is missing!"
                    }
                }
                sh '''
                cd /opt
                sudo wget https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip
                '''
            }
        }
    }
    post {
        always {
            echo 'Cleaning up temporary files...'
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
