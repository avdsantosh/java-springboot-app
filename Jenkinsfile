pipeline {
    agent {
        node {
            label 'jenkins-slave-node'
        }
    }
    
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }

    stages {
        stage("Build Stage") {
            steps {
                echo "----------- Build Started ----------"
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo "----------- Build Completed ----------"
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonar-scanner-portal'
            }
            steps {
                withSonarQubeEnv('sonar-server-portal') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}