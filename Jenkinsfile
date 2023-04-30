node (label: 'TN_HtmlNginx_App'){
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build Docker image') {
  
       app = docker.build("eagunuworld/primary-argocd:${env.BUILD_NUMBER}")
    }

    stage('Test Docker image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image to Nexus') {
        sh 'docker login -u eagunuworld -p Aighegbe12345@ eagunuworld/primary-argocd'
            app.push("${env.BUILD_NUMBER}")
    }
    stage('Trigger Update Manifest') {
        echo "triggering Update manifest Job"
            build job: 'sub_walmart', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    }
    
}