// pipeline{
//     agent { label 'node_aws'}
//     tools {
//         maven 'maven3.9'
//     }
//     stages{
//         stage('Code checkout'){
//             steps{
//                 echo "checking out code"
//                 git branch: 'main', url: 'https://github.com/ifediniru/docker_local.git'
//             }
//         }
//         stage('Maven Build'){
//             steps{
//                 echo "Building source code using Maven from Jenkins file"
//                 sh "mvn clean package"
//                 // sh "mvn package"
//                 echo "Building source code using Maven was successful"
//             }
//         }
//         stage('Sonarqube Analysis'){
//             steps{
//                 echo "Analysing Sourcecode"
//                 // sh "mvn sonar:sonar -Dsonar.qualitygate.wait=true"
//             }
//         }
//         stage('Artifact Management'){
//             steps{
//                 echo "Pushing artifacts to Nexus"
//                 // sh "mvn deploy -s ./settings.xml"
//             }
//         }
//         stage('Tomcat Deploy'){
//             steps{
//                 echo "Deploying Application to Tomcat"
//                 // sh "rm -rf '/tmp/demojenkins'"
//                 deploy adapters: [tomcat9(credentialsId: 'tomcat2', path: '', url: 'https://98df-142-198-195-76.ngrok-free.app')], contextPath: null, war: 'target/*.war'
//             }
//         }
//     }
// }










//Declarative pipeline


pipeline{
    agent any
   // agent{ label 'node_aws'
   //     }
    environment{
        BUILD_USER="Osamu Dazai"
    }
    tools{
        maven 'raven'
    }
    stages{
        stage('Checkout source code'){
            steps{
                echo "checking out code from Github"
                git branch: 'main', credentialsId: 'github_PAT', url: 'https://github.com/DevHashira/Orange-lemon.git'
                echo "checkout success"
                sh 'ls -al'
              /**  timeout(time:2, unit: "HOURS"){
                input message: 'Approve for testing'
                }
              **/ 
            }
        }

        stage('Maven build'){
            steps{
                echo 'compiling source code using maven'
                sh 'mvn clean package'
                //sh 'ls -al /Pipeline+/Workspace | grep  -Eni "target"'
                sh 'ls -al target'
            }
        }

        stage('Testing'){
            parallel{
                stage('Testing out the parallel block'){
                    steps{
                        echo "Initial parallel stage"
                        sh "sleep 10"
                    }
                }
                stage('Second phase of the parallel test'){
                    steps{
                        echo "2nd quarter initiated"
                        sh "sleep 10"
                    }
                }
                stage('3rd quarter'){
                    environment{
                        NAP="sleep 10"
                    }
                    steps{
                        echo "concluding phase of the parallel test"
                        sh "${env.NAP}"
                    }
                }
            }
        }
        
   /**    stage('SonarQube Analysis'){
            steps{
                timeout(time:1, unit: "DAYS"){
                    input message: 'Affirm approval for Sonarqube analysis'
                }
                echo "Initiating code analysis with Sonarqube"
                sh 'mvn sonar:sonar'
                echo 'Quality profile passed'
                echo 'Quality gate passed'
            }
        }

         stage('Nexus Artifactory'){
            steps{
               echo 'Deploying artifact to nexus' 
               sh 'mvn deploy -s settings.xml'
            }
        }
 **/
         stage('Tomcat Deployment'){
            steps{
                echo "Requesting permission to go green for deployment"
            /**    timeout(time: 2, unit: "HOURS"){
                 input message: 'Inquiring directives on approval'
                }
              **/
                echo 'deploying to tomcat'
            //    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat_ID', path: '', url: 'https://straddle-kerchief-scruffy.ngrok-free.dev')], contextPath: 'web-app', war: 'target/*.war'
                echo 'deployment success'
            }
        }

        post{
            always{
                emailext(
                    to: 'devhashira@outlook.com, ikeoluwaoladipupo21@gmail.com, youhavemerelyadoptedthedark@gmail.com',
                    subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "Status: ${currentBuild.currentResult}\n${env.BUILD_URL}",
                    attachLog: true
                )
            }
        }
    }
}



