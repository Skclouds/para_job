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
                    // Construct the URL for Maven
                    def mavenUrl = "https://dlcdn.apache.org/maven/maven-3/${maven_version}/binaries/apache-maven-${maven_version}-bin.tar.gz"
                    
                    // Validate Maven URL before downloading
                    sh """
                    cd /var/lib/jenkins/
                    if curl --head --silent --fail ${mavenUrl} > /dev/null; then
                        echo "Downloading Maven version ${maven_version}"
                        sudo wget ${mavenUrl}
                    else
                        echo "Error: Maven version ${maven_version} not found!"
                        exit 1
                    fi
                    """
                }
            }
        }
        stage('Download Terraform') {
            steps {
                script {
                    // Construct the URL for Terraform
                    def terraformUrl = "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip"

                    // Validate Terraform URL before downloading
                    sh """
                    cd /opt
                    if curl --head --silent --fail ${terraformUrl} > /dev/null; then
                        echo "Downloading Terraform version ${terraform_version}"
                        sudo wget ${terraformUrl}
                    else
                        echo "Error: Terraform version ${terraform_version} not found!"
                        exit 1
                    fi
                    """
                }
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
