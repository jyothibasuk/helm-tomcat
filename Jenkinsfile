pipeline {

    agent any

    stages {

        stage ('checkout') {

            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jyothibasuk/helm-tomcat.git']]])
            }
        }

        stage ('Deploy to AKS Cluster') {

            steps {
                script {
                    
                    kubernetesDeploy(
                    configs: 'k8s',
                    kubeconfigId: 'k8s-cluster',
                    )
                    sh 'helm install ./k8s --generate-name'
                }
                
            }
        }
    }
}
