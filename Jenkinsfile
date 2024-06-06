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
        withCredentials([string(credentialsId: 'dockerhubpass', variable: 'docker')]) {
        sh "docker login -u sujitha202301 -p ${docker}"
        }
    }
    stage('tag and push'){
        sh "docker tag project02 sujitha202301/spring123:1"
        sh "docker push sujitha202301/spring123:1"
    }
    stage('deploy'){
    ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: '/var/lib/jenkins/workspace/pipeline/ansible-playbook.yml', vaultTmpPath: ''
}
}
