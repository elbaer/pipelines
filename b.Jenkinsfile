pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timeout(time: 10, unit: 'MINUTES')
        timestamps()
    }
    
    stages {
        stage ('checkout component') {
            steps {
                git branch: 'master', url: 'https://github.com/elbaer/integration-pipeline.git'
            }
        }
        stage ('build') {
            steps {
                dir ('component-b') {
                    trackComponentVersions pomFile: 'pom.xml'
                }
            }
        }
        stage ('integration pipeline') {
            steps {
                build job: 'integration-pipeline', wait: false, quietPeriod: 0
            }
        }
    }
}