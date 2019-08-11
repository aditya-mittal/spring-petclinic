pipeline {
    agent any
    options {
        skipDefaultCheckout true
    }
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'LocalBranch', localBranch: 'master']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/aditya-mittal/spring-petclinic.git']]])
            }
        }
        stage('build') {
            steps {
                sh label: '', returnStatus: true, script: './mvnw package'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            junit 'target/surefire-reports/**/*.xml'
        }
    }
}
