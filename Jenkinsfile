pipeline{
    agent any 
    options{
        buildDiscarder(
            logRotator(
                numToKeepStr:'5',
                daysToKeepStr:'5',
                artifactDaysToKeepStr:'5',
                artifactNumToKeepStr:5   
            )
        )
    }
    environment{
        PATH = "C:\\Windows\\System32;C:\\Users\\muhammad.sufiyan\\AppData\\Local\\Programs\\Git\\bin"
    }
    tools{
        maven 'apache-maven-3.8.6'
        jdk 'Java-JDK'
    }
    stages{
        stage('----clean----'){
            steps{
               
                bat "mvn clean"
            }
        }

        stage('----test----'){
            steps{
                bat "mvn test"
            }
        }
        stage('----package----'){
            steps{
                bat "mvn package"
            }
        }
    }

}

