pipeline{

    agent any
    tools{
        //Calling maven version
        maven "maven3.8.6"
    }
    
    stages{
        stage('scm'){
            steps{
              echo "Get code from repository"
              git branch: 'main', credentialsId: 'maven-repo-credentials', url: 'https://github.com/markondareddy/mavenwebproject.git' 
            }
        }
        
         stage('compile'){
            steps{
              echo "Compile source code"
              sh "mvn compile"
            }
        }
        
        stage('GenerateArtifactfile'){
            steps{
              echo "Generate the artifact file"
              sh "mvn package"
            }
        }
        
         stage('Deployment'){
            steps{
              echo "Deploy artifact file into tomcat server"
              
              deploy adapters: [tomcat9(credentialsId: 'tomcat-credential', path: '', url: 'http://35.171.2.61:8080/')], contextPath: 'javawebproject', war: '**/*.war'
            
            }
        }
        
    }
    
}

