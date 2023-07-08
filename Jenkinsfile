def GITHUB_REPO = "https://github.com/gauravumrane29/spring-petclinic.git" 
def GITHUB_BRANCH = "main"
def SUBJECT = "JENKINS NOTIFICATION"
def REPLY_EMAIL = "kunalumrane@gmail.com"

pipeline{
    agent any
    stages{
        stage('clean workspace'){
            steps{
                deleteDir()
            }
        }
        stage('Version checking'){
            steps{
                sh "mvn --version"
                sh "java --version"
            }
        }
        // stage('git checkout'){
        //     steps{
        //         git branch:GITHUB_BRANCH, url: GITHUB_REPO, credentialsId: 'kunalumrane'
        //     }
        // }
        stage("build & SonarQube analysis") {
            steps {
                script{
                    withSonarQubeEnv(credentialsId: 'Sonar Token') {
                    sh 'mvn clean package sonar:sonar'
                }
              }
            }
          }
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        
    //     stage('Email Notification'){
    //     steps{
    //         script{
    //             FAILED_STAGE=env.STAGE_NAME
    //             emailext attachLog: true,
    //             body: "Successfull\n\nBuild URL: ${BUILD_URL} \n\n Build: ${BUILD_NUMBER} Build_ID:${BUILD_ID}" ,
    //             to: "${REPLY_EMAIL}",
    //             from: "Jenkins",
    //             subject: "${SUBJECT} - Build Sucessfull."
    //         }
    //     }
    
    // }
    }
}
