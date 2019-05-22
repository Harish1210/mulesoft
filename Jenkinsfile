pipeline {

    environment {

        appName = "errorPoc"

    }

    agent any

    stages {

        stage('Notify_Build_Starts'){

            steps{

                slackSend color: '#439FE0', message: "*Started Build Number:1234"

            }

        }

      	stage('Sonar_Test'){
          
          steps{

            script{
            	sh "mvn -e clean package -DattachMuleSources sonar:sonar"
            }

          }

      	}

        stage('Build_and_Test') {

            steps {

                script {

                    if(env.GIT_BRANCH.toLowerCase() == 'master') {

                        withMaven(maven: 'Maven_Jenkins_Embedded', globalMavenSettingsConfig: 'MuleSoft_Global_Settings') {

                            sh "mvn -e clean"

                        }

                    } else {

                        withMaven(maven: 'Maven_Jenkins_Embedded', globalMavenSettingsConfig: 'MuleSoft_Global_Settings'){

                            sh "mvn -e clean test"

                        }

                    }

                }

            }

        }

        stage('Deploy_to_Cloudhub') {

            steps {

                

                    withMaven(maven: 'Maven_Jenkins_Embedded', globalMavenSettingsConfig: 'MuleSoft_Global_Settings'){

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

    post {

        success {

            slackSend color: '#34ea31', message: "*Completed Build Number:*1234"

        }

        failure {

            slackSend color: '#e83036', message: "*Failed Build Number:* 1234"

        }

    }

}