def gv 

pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
    }

    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage('build') {
            steps {
                script{
                    gv.buildApp()
                }
            }
        }
        stage('test') {
            steps {
                script {
                    gv.testApp()
                }
                
            }
        }
        stage('deploy') {
            
            steps {
                script {
                    env.ENV = input message: "Select the environment to deploy to", ok: "Done", parameters: [choice(name: 'ONE', choices: ['dev', 'staging', 'prod'], description: '')]
                    gv.deployApp()
                    echo "Deploying to ${ENV}"
                    echo 'changes made for testing'
                    
                }    
            }
        }
    }
}
