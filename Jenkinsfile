int build = 1
def currentBuildNo = currentBuild.number

@Library("shared-library") _
pipeline{
    agent any
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
                script{
                      buildSettings(build)                  
                }
                helloWorld(name:"Sufiyan" , description:"How Was The Day")
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