pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    // environment { 
    //     packageVersion = ''
    //     nexusURL = '172.31.15.118:8081'
    // }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'version', defaultValue: '', description: 'What is the artifact version?')
        string(name: 'environment', defaultValue: '', description: 'What is environment?')
        // booleanParam(name: 'Destroy', defaultValue: 'false', description: 'What is Destroy?')
        // booleanParam(name: 'Create', defaultValue: 'false', description: 'What is Create?')
    }
    // build
    stages {
        stage('Print version') {
            steps {
                sh """
                    echo "version: ${params.version}"
                    echo "environment: ${params.environment}"
                """
            }
        }

        stage('Deploy') {
            steps {
                build job: "catalogue-deploy", wait: true, parameters: [string(name: 'version',value: "${packageVersion}"),
                    booleanParam(name: 'environment',value: "dev")
                ]
                
            }
        }   
        
    }
    // post build
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}