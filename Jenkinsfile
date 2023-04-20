pipeline {
    agent {
        node {
            label 'java11'
        }
    
    }

    options {
                timestamps()
                buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '2'))
                timeout(time: 240, unit: 'MINUTES')
               // disableConcurrentBuilds()
                }

        stages {
            stage ('AppCodeCheckout') {
                steps {

                    git 'https://github.com/gcpcloudreddy/pylife-devops-demo.git'

                }
            }
            stage ('CI Build') {

                steps {

                    sh 'mvn clean package'
                   
                     }
    
            }

            stage ('Docker Build && Push && DEPLOY ') {
               

                steps {
                   
                    sh 'docker build . -t anushalokiny/app30:test
                    sh 'docker login -u anushalokiny -p dckr_pat_5hqwwpAesEYjY3egx8qa8KmWa2Q'
                    sh 'docker push anushalokiny/app30:test'
                    sh 'docker run -p 99:8080 -d anushalokiny/app30:test'


                }
            
        }

            stage('Archive and clean workspace') {
                steps {
                    
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                    cleanWs()
                }

            }
        }  
}
