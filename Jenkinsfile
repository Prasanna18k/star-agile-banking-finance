node{
    stage('code_checkout')
    {
        git branch: 'master', url: 'https://github.com/Arshiyaz/banking.git'
    }
    stage('code_compile'){
    sh 'mvn compile'
    }
    stage('code_build'){
    
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t arshiya13/banking .'
   
    }
    stage('docker image push')
    {
    
    withCredentials([string(credentialsId: 'dockerid', variable: 'dockervar')]) {
        sh 'docker login -u arshiya13 -p ${dockervar}'
        sh 'docker push arshiya13/banking'
    
}
    }
    stage('ansible_deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansibleid', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}

