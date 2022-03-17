pipeline{
    agent any 
    stages{
        stage("SCM Checkout"){
            steps{
               git 'https://github.com/guruprasad-kannan/gururegistration.git'
            }
        stage("Build using maven"){
            steps{
                def mvnHome =  tool name: 'maven3', type: 'maven'   
                sh "${mvnHome}/bin/mvn clean install"
           }
        }
        }
}   }
 