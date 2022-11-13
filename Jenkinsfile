pipeline {
    agent any

    stages {
        stage('Gut hub pull stage ') {
            steps {
                script{
                    checkout([$class: 'GitSCM' , branches: [[name: '*/master']] ,
                       userRemoteConfigs: [[
                           credentialsId: 'Githubcredentials',
                           url :'https://github.com/Zeroxcharisma/Angular2.git']]])
                }
            
            }
        }
      stage('Build Stage ') {
            steps {
                script{
                    
                    sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml -e ansible_become_password=root "
                }}}
      stage('Docker build image ') {
            steps {
                script{
                    sh "ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml -e ansible_become_password=root "
                }}}
      stage('docker push image') {
            steps {
                script{
                    sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml -e ansible_become_password=root"
                }}}
    }
}
