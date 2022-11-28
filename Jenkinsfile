pipeline{
    agent any 
    options{
        buildDiscarder(
            logRotator(
                numToKeepStr:'5',
                daysToKeepStr:'5',
                artifactDaysToKeepStr:'5',
                artifactNumToKeepStr:'5'   
            )
        )
    }
    environment{
        PATH = "C:\\Windows\\System32;"
    }
    tools{
        maven 'apache-maven-3.8.6'
        jdk 'Java-JDK'
        git 'git-latest'
    }
    stages{
        stage('----parameters----'){
            steps{
                script{
                    properties([
                        parameters([
                            string(
                                defaultValue:'1.0.73',
                                name:'UREBAL_VERSION',
                                description:'UREBAL project version, defaults to 1.0.0',
                                trim:false
                            ),
                            string(
                                defaultValue:'.1',
                                name:'UR_BUILD_VERSION',
                                description:'Build version for Job',
                                trim:false
                            ),
                            string(
                                defaultValue:'integration_testing',
                                name:'DatabaseName',
                                description:'Name of configured oracle schema user',
                                trim:false
                            ),
                            string(
                                defaultValue:'integration_testing',
                                name:'DatabaseName',
                                description:'Name of configured oracle schema user',
                                trim:false
                            ),
                            password(
                                name:'DatabasePassword',
                                description:'integration_testing',
                            ),
                            string(
                                defaultValue:'192.168.2.45/ORCL',
                                name:'DatabaseServer',
                                description:'Hostname and service name for configured schema',
                                trim:false
                            ),
                            choice(
                                choices:['BLUELEAF' , 'PROD-V2'],
                                name:'FRONTEND'
                            )
                        ])
                    ])
                }
            }
        }
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

