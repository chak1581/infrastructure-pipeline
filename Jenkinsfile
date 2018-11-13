properties([pipelineTriggers([githubPush()])])
node('linux') {
    git url: 'https://github.com/chak1581/infrastructure-pipeline.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
}
