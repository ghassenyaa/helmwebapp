node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    dir('webapp1') {

                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email yaaghassen@gmail.com"
                        sh "git config user.name ghassenyaa"
                        sh "git fetch origin"
                        sh "git checkout origin/main" // Checkout the remote branch
                        //sh "git switch master"
                        sh "cat values.yaml"
                        sh "sed -i 's/^\\(\\s*tag:\\s*\\).*/\\1${DOCKERTAG}/' values.yaml"
                        sh "cat values.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push origin HEAD:main https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git"
                    }

      }
    }
  }
}
}