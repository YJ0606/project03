node{
    stage('git code checkout'){
        echo 'checkout the code from git repository'
        git 'https://github.com/sujitharamesh1998/project02'
        echo 'completed'
        }
    stage('build'){
        sh "mvn clean package"
    }
    stage('creating docker'){
        sh "docker build -t project02 ."
    }
    stage('docker login'){
    withCredentials([string(credentialsId: 'dockerhubpass', variable: 'dockerhub')]) {
    sh " docker login -u yash3033 -p ${dockerhub} "
        }
    }
    stage('tag and push'){
        sh "docker tag project02 yash3033/staragileproject:3"
        sh "docker push yash3033/staragileproject:3"
    }
    stage('deploy in test server'){
    ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: '/var/lib/jenkins/workspace/pipeline/ansible-playbook.yml', vaultTmpPath: ''
}    
}
