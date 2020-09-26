node{
    def docker = tool name: 'docker', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
    def dockerCMD = “{$docker}/bin/docker”

    stage('git checkout'){
        git 'https://github.com/bhar-subhajit/cicd-pipline-bootcamp.git'
    }
    
    stage('build and test'){
        def mavenHome = tool name: 'maven-3', type:'maven'
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
     
    }
    
    stage('docker build'){
        sh "{$dockerCMD} build -t subhajit1996/java-app:1.0.0 ." 
        
    }
    
    stage('push docker image to docker hub'){
        withCredentials([string(credentialsId: 'dockerHubPassword', variable: 'dockerHubPwd')]) {
            sh "{$dockerCMD} login -u subhajit1996 -p ${dockerHubPwd}"
        }
        sh "{$dockerCMD} push subhajit1996/java-app:1.0.0"
    }
    
    stage('run docker image'){
        sh "{$dockerCMD} run -p 8888:8080 -d subhajit1996/java-app:1.0.0"
    }
}
