node{
       stage('scm checkout')
       {
git (credentialsId: 'github',
url: 'https://github.com/neelimak2020/docker-jenkins.git',
branch:'master')
}
       
  stage('Build DockerImage'){
sh 'docker --version'
}
     

stage('Build DockerImage'){
sh 'docker build -t neelima2020/my-app:1.0.0 .'
}

stage('Push Docker Image'){

withCredentials([string(credentialsId: 'DockerPWD', variable: 'DockerPWD')]) {
    sh "docker login -u neelima2020 -p ${DockerPWD}"
}
sh 'docker push neelima2020/my-app:1.0.0'
}

stage('run container on server')
{
       sh 'docker pull neelima2020/my-app:1.0.0'
def dockerRun='docker run -p 80:8080 d -name my-app neelima2020/my-app:1.0.0'

     sshagent(['sshkey']) {

       sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.19.240 ${dockerRun}"

}
}

}


