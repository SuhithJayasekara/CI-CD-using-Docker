pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp 34341755/samplewebapp:latest'
                
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        	    sh  'docker logout'
		    sh 'docker login -u 34341755 -p 34341755suhith'
		    sh  'docker push 34341755/samplewebapp:latest'
		   
                  
          }
        }
     
      stage('Run Docker container on EC2 Instance ') {
             
            steps 
	      {
                 def dockerrun= "docker run -d -p 8003:8080 34341755/samplewebapp"
		 sshagent(['suhith-docker']) {
  			sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.18.198 ${dockerrun}'
}
 
            }
        }
 
    }
	}
    
