pipeline {

    agent { label 'JDK17' }

    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'clean package', description: 'Enter Maven goal to run')
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        retry(2)
    }

    stages {

        stage('Git clone') {
            steps {
                git url: 'https://github.com/Roop-14/spring-petclinic.git', branch: 'main'
            }
        }

        stage('Build the code') {
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }

        stage('Reporting and Archiving') {
            steps {
                junit testResults: 'target/surefire-reports/*.xml'
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo "Build SUCCESS"
        }
        unsuccessful {
            echo "Build FAILED"
        }
    }
}

