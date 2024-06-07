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
    sh " docker login -u sujitha202301 -p ${dockerhub} "
        }
    }
    stage('tag and push'){
        sh "docker tag project02 sujitha202301/staragileproject:3"
        sh "docker push sujitha202301/staragileproject:3"
    }
}    
