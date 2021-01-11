podTemplate(containers: [
    //containerTemplate(name: 'aws-ansi', image: 'aws-ansi-tf-agent:v3', alwaysPullImage: false, ttyEnabled: true, command: 'cat'),
    //containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true)
    containerTemplate(name: 'helm-agent', image: 'helm-skaffold:v1', command: 'cat', ttyEnabled: true)
    ],
    volumes: [
        hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
    node(POD_LABEL) {
        stage('Check awscli version') {
            container('helm-agent') {
                sh "helm version"
            }
        }
        stage('Check terraform version') {
            container('helm-agent') {
                sh "skaffold version"
            }
            
        }
    }
}