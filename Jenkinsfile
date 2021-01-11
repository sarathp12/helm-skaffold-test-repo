podTemplate(containers: [
    //containerTemplate(name: 'aws-ansi', image: 'aws-ansi-tf-agent:v3', alwaysPullImage: false, ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'helm-agent', image: 'skaffold-helm-agent:v2', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true)
    ],
    volumes: [
        hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
    node(POD_LABEL) {
        stage('Check awscli version') {
            container('helm-agent') {
                sh "helm version"
                sh "skaffold version"
            }
        }
        stage('Check terraform version') {
            container('helm-agent') {
                withAWS(credentials:'aws-id') {
                    aws ecr get-login-password --region "us-east-2" | docker login --username AWS --password-stdin '471574026140.dkr.ecr.us-east-2.amazonaws.com/test-psp-repo'
                }
                //sh "aws ecr get-login"
            }
            
        }
    }
}