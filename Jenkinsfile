node{
    stage('git checjout')
    {
        git branch: 'master', url: 'https://github.com/chandanadevopslearn/insure-me.git'
    }

    stage('build'){
    
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t mchandana123/insureme:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'docker-password', variable: 'docker')]) {
        sh 'docker login -u mchandana123 -p ${docker}'
        sh 'docker push mchandana123/insureme:1.0'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
