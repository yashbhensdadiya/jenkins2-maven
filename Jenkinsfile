pipeline {
    agent any
    tools {
        maven 'maven3.9'
        jdk 'java17'
    }
    stages {
        stage('Git-Code-Download') {
            steps {
                echo "Downloading code from git"
                git branch: 'main', url: 'https://github.com/yashbhensdadiya/jenkins2-maven.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Going to java project using maven'
                sh 'mvn clean package'
            }
        }
        stage('Test-Case') {
            steps {
                echo 'check test cases'
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }
        }
        stage('Archive-Artifacts') {
            steps {
                echo 'Archiving the Artifacts'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Deploy-to-Dev') {
            steps {
                echo 'Deploy'
                build wait: false, job: 'Deploy-to-Dev-Popeline'           
            }
        }    
    }
}
