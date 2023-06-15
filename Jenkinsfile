node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                  withCredentials([sshUserPrivateKey(credentialsId: '9a987cbd-6fc0-4c34-952b-910e9c96798f', keyFileVariable: 'SSH_KEY')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email dragonus282@gmail.com"
                        sh "git config user.name dragonus282"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+035296596762.dkr.ecr.ap-southeast-1.amazonaws.com/gitops-sample-app.*+035296596762.dkr.ecr.ap-southeast-1.amazonaws.com/gitops-sample-app:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git checkout main"
                        sh 'GIT_SSH_COMMAND="ssh -i $SSH_KEY" git push git@github.com:longle2/gitops_sample_manifest.git'
                    }
                    // withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    //     //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                    //     sh "git config user.email dragonus282@gmail.com"
                    //     sh "git config user.name dragonus282"
                    //     //sh "git switch master"
                    //     sh "cat deployment.yaml"
                    //     sh "sed -i 's+035296596762.dkr.ecr.ap-southeast-1.amazonaws.com/gitops-sample-app.*+035296596762.dkr.ecr.ap-southeast-1.amazonaws.com/gitops-sample-app:${DOCKERTAG}+g' deployment.yaml"
                    //     sh "cat deployment.yaml"
                    //     sh "git add ."
                    //     sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    //     sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitops_sample_manifest.git HEAD:main"
      }
    }
  }
}
