node{
    stage('git checjout')
    {
        git branch: 'master', url: 'https://github.com/chandanadevopslearn/insure-me.git'
    }

    stage('build'){
    
    sh 'mvn clean package'
    }
    stage('test'){
        
    sh 'mvn test'
        
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t mchandana123/insureme:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerpwd')]) {
        sh 'docker login -u mchandana123 -p ${dockerpwd} '
    
}
        sh 'docker push  mchandana123/insureme:1.0 '
    }
    stage('deploy')
    {
    
       ansiblePlaybook credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'myansible', inventory: 'hosts', playbook: 'ansible-playbook.yml'
    }
}
