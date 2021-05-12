pipeline {
    agent any
    stages {
        stage('Main') {
            when { branch 'main' }
            steps {
                echo "Building Main Branch"
                checkout scm
                tektonCreateRaw(
                        input: ".lighthouse/jenkins-x/release.yaml", 
                        inputType: "FILE", 
                        namespace: 'tekton-pipelines',
                        enableCatalog: true)
            }
        }
        stage('PR') {
            when { changeRequest() }
            steps {
                echo "Building PR"
                checkout scm
                tektonCreateRaw(
                        input: ".lighthouse/jenkins-x/pullrequest.yaml", 
                        inputType: "FILE", 
                        namespace: 'tekton-pipelines',
                        enableCatalog: true)
            }
        }
    }
}
