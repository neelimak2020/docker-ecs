node{
       stage('scm checkout')
       {
git (credentialsId: '55fd54ac-8a3a-4ec2-8158-bdb59e33ee47',
url: 'https://github.com/neelimak2020/docker-ecs.git',
branch:'master')
}

stage('Build DockerImage'){
sh 'docker build -t neelima2020/my-app:1.0.0 .'
}

stage('Push Docker Image'){

withCredentials([string(credentialsId: 'Docker-PWD', variable: 'DockerPWD')]) {
    sh "docker login -u neelima2020 -p '${DockerPWD}"
}
sh 'docker push neelima2020/my-app:1.0.0'
}

stage('run container on server')
{
def dockerRun='docker run -p 80:80800d -name my-app neelima2020/my-app:1.0.0'

withCredentials([
sshUserPrivateKey(credentialsId: 'ec2-server', 
keyFileVariable: 'ec2key',
usernameVariable: 'ec2-user'
)]) {
sh 'ssh -o StrickHostKeyChecking=no ec2-user@ -i ec2key ${dockerRun}'  

sh 'docker run -p 80:80800d -name my-app neelima2020/my-app:1.0.0'
}
}

}


