node {
    
     def app

    stage('Clone Repository') {
        steps {
            checkout scm
        }
    }

    stage('Update GIT') {
        steps {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'GIT_HUB_CREDENTIALS', variable: 'git hub credential')]) {
                        sh "git config user.email betiniawara@gmail.com"
                        sh "git config user.name bertiniawara"

                        sh "cat deployment.yaml"
                        // sh "sed -i 's+betiniawara842/kubernetes1.*+betiniawara842/kubernetes1:${env.BUILD_NUMBER}+g' deployment.yaml"
                        sh "sed -i 's+betiniawara842/kubernetes1.*+betiniawara842/kubernetes1:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push origin HEAD:main" 
                    }
                }
            }
        }
    }
}
