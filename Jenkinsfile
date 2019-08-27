pipeline{
    agent any
    stages{
        stage("AZ - Config resource"){
            agent {
                docker {
                    image "adfinissygroup/terraform-azure"
                    args "--entrypoint='' -u root"
                }
            }
            steps{
                withCredentials([azureServicePrincipal('AZURE_TERRAFORM_TEST')]) {
                    sh "az login --service-principal -u ${AZURE_CLIENT_ID} -p ${AZURE_CLIENT_SECRET} --tenant ${AZURE_TENANT_ID}"
                    sh "chmod +x scripts/tfstate_config.sh"
                    sh "source scripts/tfstate_config.sh"
                }
            }
        }
    }
}