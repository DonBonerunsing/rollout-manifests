node {
    def app
    
    env.IMAGE = 'danny1dockerhub/argo-rollout-bluegreen'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/DonBonerunsing/rollout-manifests.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'danny-git', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        sh "git config user.email dandevops2023@gmail.com"
                        sh "git config user.name Daniel"
                        //sh "git switch master"
                        sh "cat rollout.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' rollout.yml"
                        sh "cat rollout.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job Rolloutmanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/rollout-manifests.git HEAD:main"
             }
         }
     }
  }
}
