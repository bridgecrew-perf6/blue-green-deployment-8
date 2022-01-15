stage("Git Clone"){

        git branch: 'blue', credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/prudhviraaz14/blue-green-deployment'
    }
stage('Build image') {
        sh 'docker version'
        sh 'docker build -t mywebapp .'
        sh 'docker image list'
        sh 'docker tag mywebapp prudhviraaz14/mywebapp:mywebapp'
}
stage(Push image') {
      sh 'docker push  prudhviraaz14/mywebapp:mywebapp'
}
stage('create the kubeconfig file') {
                kubernetesDeploy(
                    kubeconfigId: 'K8S',
                    enableConfigSubstitution: true
                    )           
}
stage('Deploy blue container') {
  when { branch 'blue'}
}
stage('Redirect service to blue container') {
  when { branch 'blue'}
}
stage('Deploy green container') {
  when { branch 'green'}
}
stage('Redirect service to green container') {
  when { branch 'green'}
}
