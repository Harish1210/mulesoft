pipeline {

    environment {

        appName = "errorPoc"

    }

    agent any

    stages {


      	

        stage('Compile') {

            steps {

                
                   

                        withMaven(maven: 'Maven') {

                            sh "mvn clean compile"

                       
                            }
                    } 

                    }


          

        stage('Deploy_to_Cloudhub') {

            steps {

                

                    withMaven(maven: 'Maven'){

                        sh "mvn deploy"

                    
                }

            }

        }

        stage('CleanUp') {

            steps {

                cleanWs notFailBuild: false

            }

        }

    }

   

}