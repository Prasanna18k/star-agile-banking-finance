node{
    stage('code_checkout')
    {
        git branch: 'master', url: ''
    }
    stage('code_compile'){
    sh 'mvn compile'
    }
    stage('code_build'){
    
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t prasannagundavarapu/banking .'
   
    }
    stage('docker image push')
    {
    
    withCredentials([string(credentialsId: 'dockerid', variable: 'dockervar')]) {
        sh 'docker login -u prasannagundavrapu-p ${dockervar}'
        sh 'docker push prasannagundavrapu/banking'
    
}
    }
    stage('ansible_deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansibleid', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}

