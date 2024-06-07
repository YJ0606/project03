node{
    stage('git code checkout'){
        echo 'checkout the code from git repository'
        git 'https://github.com/sujitharamesh1998/project02'
        echo 'completed'
        }
    stage('build'){
        sh "mvn clean package"
    }
      stage('docker'){
        sh "docker build -t project02 ."
    }
    stage('login'){
    withCredentials([string(credentialsId: 'docker', variable: 'dockerlogin')]) {
    sh " docker login -u sujitha202301 -p ${dockerlogin}"
       }
    }
    stage('tag'){
        sh " docker tag project02 sujitha202301/staragileproject:1 "
        sh " docker push sujitha202301/staragileproject:1 "
    }
    stage('deploy'){
     ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: '/var/lib/jenkins/workspace/pipeline/ansible-playbook.yml', vaultTmpPath: '' 
    }
    
}        
