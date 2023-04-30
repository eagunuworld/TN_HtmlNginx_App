node (label: 'TN_HtmlNginx_App'){
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build Docker image') {
  
       app = docker.build("http://34.174.116.217:8585/eagunu/repository/argocd-demo:${env.BUILD_NUMBER}")
    }

    stage('Test Docker image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image to Nexus') {
        sh 'docker login -u admin -p passw0rd http://34.174.116.217:8585/eagunu/repository/argocd-demo/'
            app.push("${env.BUILD_NUMBER}")
    }
    stage('Trigger Update Manifest') {
        echo "triggering Update manifest Job"
            build job: 'argocd-update-manifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    }
    
}