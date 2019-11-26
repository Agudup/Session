@Library('piper-lib-os') _

pipeline {

    agent any

    stages {
        stage("prepare") {
            steps {
                deleteDir()
                checkout scm
                setupCommonPipelineEnvironment script: this
            }
        }
        stage('build') {
            steps {
                mtaBuild script: this, buildTarget: 'XSA'
            }
        }
        stage('deploy') {
            steps {
                xsDeploy script: this, apiUrl: 'https://10.79.9.18:30030', org: 'orgname', space: 'PROD',docker: [dockerImage:5f84aab33ccd, dockerPullImage:false], loginOpts:  '--skip-ssl-validation'
            }
        }
    }
}
