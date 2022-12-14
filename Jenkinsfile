

@Library("shared-library") _
pipeline{
    agent {
        label 'default_node'
    } 
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
        PATH = "C:\\Windows\\System32;C:\\Program Files (x86)\\pgAdmin 4\\v4\\runtime;C:\\Program Files\\PuTTY"
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
        stage('----print-----'){
           steps{
                bat "echo UREBAL_VERSION : " + params.UREBAL_VERSION
                bat "echo UR_BUILD_VERSION : " + params.UR_BUILD_VERSION
                bat "echo DatabaseName : " + params.DatabaseName
                bat "echo DatabasePassword : " + params.DatabasePassword
                bat "echo DatabaseServer : " + params.DatabaseServer
                bat "echo FRONTEND : " + params.FRONTEND
           }
        }
        stage('-----db----'){
            steps{
                // For Drop And Creating Tables
                bat dbSettings("C:\\URebal\\UR-PRO-Backend\\" , "jenkin_db" , "src\\DB Scripts\\PostgreSQL\\Complete" , "DropCreateTables" , false , [:])

                // For Passing Default Data
                bat dbSettings("C:\\URebal\\UR-PRO-Backend\\" , "jenkin_db" , "src\\DB Scripts\\PostgreSQL\\Complete" , "DefaultData" , false , [:]) 

                // For Creating Stored Procedures and Functions
                bat dbSettings("C:\\URebal\\UR-PRO-Backend\\" , "jenkin_db" , "src\\DB Scripts\\PostgreSQL\\Complete" , "StoredProceduresAndFunctions" , false , [:])

                // For Creating Views
                bat dbSettings("C:\\URebal\\UR-PRO-Backend\\" , "jenkin_db" , "src\\DB Scripts\\PostgreSQL\\Complete" , "Views" , false , [:])

                // For Creating Firm
                bat dbSettings("C:\\URebal\\UR-PRO-Backend\\" , "jenkin_db" , "src\\DB Scripts\\Blueleaf" , "CreateFirm2" , true , ["firmName":"jenkin_firm"])

                // For Creating User
                bat dbSettings("C:\\URebal\\UR-PRO-Backend\\" , "jenkin_db" , "src\\DB Scripts\\Blueleaf" , "CreateUser2" , true , ["firmName":"jenkin_firm" , "userId":"Sufiyan" , "userFirstName":"Sufiyan" , "userEmail":"Sufiyan@matrix.com"])
                 
            }
        }
        stage('----remote-----'){
            steps{
                bat "echo y|plink marsdev@192.168.56.102 -pw marsdev  rm -rf /home/marsdev/Desktop/*.txt"

                bat "pscp -pw marsdev -P 22 C:\\Users\\muhammad.sufiyan\\Desktop\\*.txt marsdev@192.168.56.102:/home/marsdev/Desktop"

                bat "pscp -pw marsdev -P 22 C:\\Users\\muhammad.sufiyan\\Documents\\NetBeansProjects\\test_jenkins\\dist\\test_jenkins.war marsdev@192.168.56.102:/home/marsdev/web/apache-tomcat-8.5.84/webapps"
                
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

