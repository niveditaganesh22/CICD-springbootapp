pipeline {
    agent any
    tools {
        maven 'Maven-Jenkins' // Ensure this matches your Maven installation name in Jenkins
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner' // Ensure this matches your Sonar Scanner tool name in Jenkins
    }
    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/niveditaganesh22/CICD-springbootapp.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Unit Test') {
            steps {
                echo '<----------------------Unit Test Under Progress-------------------->'
                sh 'mvn surefire-report:report'
                echo '<----------------------Unit Test Finished------------------------->'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarCloud') { // Ensure this matches your SonarQube server configuration name in Jenkins
                        sh '''
                            $SCANNER_HOME/bin/sonar-scanner \
                            -Dsonar.projectName=CICD-springbootapp \
                            -Dsonar.projectKey=niveditaganesh22_CICD-springbootapp
                        '''
                    }
                }
            }
        }
        // Uncomment and configure this stage if you need to wait for the SonarQube Quality Gate status
        // stage('Quality Gate') {
        //     steps {
        //         script {
        //             waitForQualityGate abortPipeline: false, credentialsId: 'sonar' // Ensure this matches your credentials ID for SonarQube
        //         }
        //     }
        // }
    }
}
