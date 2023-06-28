node{
    stage('git checjout')
    {
        git branch: 'master', url: 'https://github.com/Arshiyaz/banking.git'
    }

    stage('build'){
    
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t arshiya13/banking .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockerid', variable: 'dockervar')]) {
        sh 'docker login -u arshiya13 -p ${dockervar}'
        sh 'docker push arshiya13/banking'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansibleid', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}

