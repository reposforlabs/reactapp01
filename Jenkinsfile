node {   
    stage('SCM') {
        git credentialsId: 'github-reposforlabs', url: 'https://github.com/reposforlabs/reactapp01.git', branch: 'main'
    }
    
    stage('Build image') {
       dockerImage = docker.build("cloudops06/reactapp01:latest")
    }
    
    stage('Push image') {
       withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ]) {
       dockerImage.push()
        }
    }    

    stage('Stop and Kill existing container with same name if any') {
        sh "docker rm -f reactapp01"
    }
        
    stage('Run the container Locally on the Jenkins server') {
        sh "docker run -itd --name reactapp01 -p 80:80 cloudops06/reactapp01:latest"
     
    }
  }

