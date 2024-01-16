node {
    def app
    
    env.IMAGE = 'patdada/amazon'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/patdada/argocd-amazon-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'patdada-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        //script  {def IMAGE='patdada/amazon'}
                        sh "git config user.email patrickdada82@gmail.com"
                        sh "git config user.name patdada"
                        //sh "git switch master"
                        sh "cat deployment.yml"
                        sh "sed -i 's+${env.IMAGE}.*+${env.IMAGE}:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-amazon-manifest.git HEAD:main"
             }
         }
     }
  }
}
