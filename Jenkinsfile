pipeline{
    agent any 
    stages{      
             stage("Build using maven"){
            steps{
                script{
                   def mvnHome =  tool name: 'maven3', type: 'maven'   
                   sh "${mvnHome}/bin/mvn clean install"
                }                
           }
        }
              stage("Sonar Qality check"){
            steps{
                script{
                   def mvnHome =  tool name: 'maven3', type: 'maven'
	               withSonarQubeEnv('sonar') { 
	               sh "${mvnHome}/bin/mvn sonar:sonar"
                }                
           }
        }
    } 
            stage("Build using docker"){
            steps{
                script{
                    sh 'docker build -t guruprasad1996/registrationapp:v2 .'
                }                
           }
        }
              stage("Pushing image to dockerhub"){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerpass', variable: 'dockerPassword')]) {
                   sh "docker login -u guruprasad1996 -p ${dockerPassword}"
                  }
                   sh 'docker push guruprasad1996/registrationapp:v2'
                    }
                }                
           }
            stage("Remove previous container"){
                steps{
                   script{
                     try{
		              sh 'docker rm -f tomcattest'
	                    }catch(error){
		                   //  do nothing if there is an exception
	                    }
                    }
                }
            } 
            stage("Deployment"){
                steps{
                   script{
                      sh 'docker run -d -p 8090:8080 --name tomcattest guruprasad1996/registrationapp:v2'
                    }
                }
            } 



    }                
}

        


    