pipeline {
   agent{
      label "BI_NumericDemo_App"
       }

    def app
    //    options {
    //      buildDiscarder logRotator( artifactDaysToKeepStr: '1', artifactNumToKeepStr: '2', daysToKeepStr: '1', numToKeepStr: '2')
    //      timestamps()
    //     }

    //  parameters {
    //       choice choices: ['main', 'owasp_zap_api_scanning', 'lab_mutation_Test'], description: 'This is choice paramerized job', name: 'BranchName'
    //       string defaultValue: 'Eghosa DevOps', description: 'please developer select the person\' name', name: 'personName'
    //     }

   environment {
            // DEPLOY = "${env.BRANCH_NAME == "python-dramed" || env.BRANCH_NAME == "master" ? "true" : "false"}"
            // NAME = "${env.BRANCH_NAME == "python-dramed" ? "example" : "example-staging"}"
            // VERSION = "${env.BUILD_ID}"
            REGISTRY = 'eagunuworld/primary-argocd'
            imageName = "eagunuworld/primary-argocd:${BUILD_ID}"
            REGISTRY_CREDENTIAL = 'eagunuworld_dockerhub_creds'
            // westdDeploy = "west-prod-pod"
            // westCon = "west-prod-con"
            // svcPort = "30005"
            // svcName = "west-prod-svc"
            // jenkinsURL = "http://34.125.210.113"
            // serverURL = "34.174.90.141"
            // appURI = "increment/99"
          }

  stages {
    stage('Clone repository') {
      steps {
        sh "checkout scm"
      }
    }

   stage('Push Docker Image To DockerHub') {
        steps {
            withCredentials([string(credentialsId: 'eagunuworld_dockerhub_creds', variable: 'eagunuworld_dockerhub_creds')])  {
              sh "docker login -u eagunuworld -p ${eagunuworld_dockerhub_creds} "
              sh 'docker build -t ${REGISTRY}:${VERSION} .'
                }
                 sh 'docker push ${REGISTRY}:${VERSION}'
              }
          }

    
//  stage('Kindly Review And Approve West-Prod?') {
//       steps {
//         timeout(time: 2, unit: 'DAYS') {
//           input 'Do you want to Approve the Deployment to West Production Environment/Namespace?'
//         }
//       }
//     }

 
//   stage('OWASP ZAP - DAST') {
//       steps {
//           sh 'bash zap.sh'
//         }
//       }

    }
 
}