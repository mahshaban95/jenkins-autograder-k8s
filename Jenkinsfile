pipeline{
  agent any
  stages{
    stage('Clone repository') {
        steps{
            script{
                checkout scm
            }
        }
    }
    stage('Update GIT') {
        steps{
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email 'mahshaban95@gmail.com'"
                        sh "git config user.name 'Mahmoud Shaaban'"
                        //sh "git switch master"
                        sh "cat pod-with-service.yml"
                        sh "sed -i 's+mahshaban95/autograder-jenkins.*+mahshaban95/autograder-jenkins:${DOCKERTAG}+g' pod-with-service.yml"
                        sh "cat pod-with-service.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/jenkins-autograder-k8s.git HEAD:main"
                }
              }
            }
        }
    } 
  }
}