node {
    stage('SCM Checkout'){
        git url: 'https://github.com/chaoqiao/simple-maven-webapp.git', credentialsId: '', branch: 'master'
    }
    stage('MVN Build'){
        def mvnHome=tool name: 'Maven', type: 'maven'
        def mvnCMD="${mvnHome}/bin/mvn"
        sh "${mvnCMD} clean install package"
    }
    stage('Build Docker Image'){
        sh 'docker build -t chaoqiao/myapp:v1.0.1 .'
    }
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DockerHubPWD', variable: 'DockerPWD')]) {
           sh "docker login -u chaoqiao -p ${DockerPWD}"
           sh 'docker push chaoqiao/myapp:v1.0.1'
        }
    }
    stage('Run Container on Dev Server'){
        def CMD="docker run -d --name=myapp2 -p:80:8080 chaoqiao/myapp:v1.0.1"
        sshagent(['AWSKey']) {
            sh "ssh ec2@3.89.39.1 -o StrictHostKeyChecking=no $CMD"
        }
    }
}