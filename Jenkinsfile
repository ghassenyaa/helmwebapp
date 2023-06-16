node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email yaaghassen@gmail.com"
                        sh "git config user.name ghassenyaa"
                    dir('webapp1') {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        //sh "git switch master"
                        sh "cat values.yaml"
                        sh "sed -i '0,/^\\(\\s*tag:\\s*\\).*\$/s//\\1${DOCKERTAG}/' values.yaml"
                        sh "cat values.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/helmwebapp.git HEAD:main"
                    }
      }
    }
  }
}
}