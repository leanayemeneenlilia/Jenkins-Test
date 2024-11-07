node {
    def mvnHome = tool 'maven-3.5.2'
    def dockerImage
    def dockerImageTag = "devopsexample${env.BUILD_NUMBER}"
    
    stage('Clone Repo') {
        git 'https://github.com/leanayemeneenlilia/Jenkins-Test.git'
    }
    
    stage('Build Project') {
        bat "\"${mvnHome}\\bin\\mvn\" -B -DskipTests clean package"
    }
    
    stage('Initialize Docker') {
        def dockerHome = tool 'MyDocker'
        env.PATH = "${dockerHome}\\bin;${env.PATH}"
    }
    
    stage('Build Docker Image') {
        bat "docker -H tcp://127.0.0.1:2375 build -t devopsexample:${env.BUILD_NUMBER} ."
    }
    
    stage('Deploy Docker Image') {
        echo "Docker Image Tag Name: ${dockerImageTag}"
        bat "docker -H tcp://127.0.0.1:2375 run --name devopsexample -d -p 2222:2222 devopsexample:${env.BUILD_NUMBER}"
    }
}
