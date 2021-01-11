podTemplate(containers: [
    //containerTemplate(name: 'aws-ansi', image: 'aws-ansi-tf-agent:v3', alwaysPullImage: false, ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'helm-agent', image: 'skaffold-helm-agent:v2', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true)
    ],
    volumes: [
        hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
    //def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-id']]
    node(POD_LABEL) {
        
        stage('Check awscli version') {
            container('helm-agent') {
                sh "helm version"
                sh "skaffold version"
                
                def awsEcrPwd = withAWS(credentials: 'aws-direct', region: 'us-east-2') {
                        sh "aws ecr get-login-password --region \"us-east-2\" >> mypwd.txt"

                }
                
            }
        }
        stage('Check terraform version') {
            container('docker') {

                sh "echo \"I am Running\" && ls"

                /*
                sh "apk add curl"
                sh '''
                    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" &&\
                    unzip awscliv2.zip
                    '''
                sh "./aws/install"
                withAWS(credentials: 'aws-direct', region: 'us-east-2') {
                        sh "aws ecr get-login-password --region \"us-east-2\" | docker login --username AWS --password-stdin 471574026140.dkr.ecr.us-east-2.amazonaws.com/test-psp-repo"

                }
                

                //sh "docker login --username AWS --password ${awsEcrPwd} 471574026140.dkr.ecr.us-east-2.amazonaws.com/test-psp-repo"    
            
                
                sh "mkdir ~/.aws"
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-id', accessKeyVariable: 'Access Key ID', secretKeyVariable: 'Secret Access Key']]) {
                    sh "echo \"[login-profile]\" >> ~/.aws/credentials"
                    sh "echo \"AWS_ACCESS_KEY_ID: ${accessKeyVariable}\" >> ~/.aws/credentials"
                    sh "echo \"AWS_SECRET_ACCESS_KEY: ${secretKeyVariable}\" >> ~/.aws/credentials"

                }
                sh "aws configure set region \"us-east-2\" --profile login-profile"
                sh "aws ecr get-login"
                */
            }
            
        }
    }
}