//def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId:'sharkscreds']]

pipeline {
    agent any 
    environment {
        PATH = "${PATH}:${getTerraformPath()}"
        }
    stages{
            stage('test AWS credentials') {
            steps {
                withAWS(credentials: 'sharkscreds', region: 'us-east-2') {
                }
            }
        }
        stage( 'Create S3 bucket'){
            steps{
                script{
                    createS3Bucket('sharks-test-terraform123')
                }
            }
        }
        stage('Terraform init'){
            steps{
                sh "terraform init"
            }
        }
    }   
}

def getTerraformPath(){
    def tfHome = tool name: 'terraform', type: 'terraform'
    return tfHome
}

def createS3Bucket(bucketName){
    sh returnStatus: true, script: 'aws s3 mb ${bucketName} --region=us-east2'
}