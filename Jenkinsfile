node{
    stage('git checkout'){
        git 'https://github.com/bhar-subhajit/cicd-pipline-bootcamp.git'
    }
    
    stage('build and test'){
        def mavenHome = tool name: 'maven-3', type:'maven'
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
     
    }
    
    stage('docker build'){
        // def dockerHome = tool name: 'docker', type:'docker'
        // def dockerCMD = "${dockerHome}/bin/docker"
        sh 'docker build -t subhajit1996/java-app:1.0.0 .' 
        
    }
    
    stage('push docker image to docker hub'){
        withCredentials([string(credentialsId: 'dockerHubPassword', variable: 'dockerHubPwd')]) {
            sh "docker login -u subhajit1996 -p ${dockerHubPwd}"
        }
        sh 'docker push subhajit1996/java-app:1.0.0'
    }
    
    stage('run docker image'){
        sh 'docker run -p 8888:8080 -d subhajit1996/java-app:1.0.0'
    }
}
