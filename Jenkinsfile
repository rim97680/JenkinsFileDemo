pipeline{
    tools{
        maven 'mymaven'
    }
    agent any
    
    stages{
        stage('Get the code -clone repo'){
            steps{
                git 'https://github.com/rim97680/DevOpsCodeDemo.git'
            }
        }
        stage('Build the code'){
            steps{
                sh 'mvn clean install package'
            }
        }
        
        stage('copy the war in the same dir of dockerfile ( form target to current directoy)'){
            steps{
                sh 'cp /var/lib/jenkins/workspace/CICDPipeline/target/addressbook.war .'
             
            }
        }
        
        stage ('Build image'){
            steps{
               sh 'docker build -t mycicdimg:$BUILD_NUMBER .'
            }
        }
        
        stage('Run the image '){
            steps{
                sh 'docker run -d -P mycicdimg:$BUILD_NUMBER'
                sh 'docker ps -a'
            }
        }
        
    }
}
