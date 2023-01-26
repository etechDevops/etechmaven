pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('1-git-clone'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'apex-engr', url: 'https://github.com/tunde-me/etechmaven.git']])
            }
        }
        stage('2-cleanws'){
            steps{
                sh 'mvn clean'
            }
        }
        stage('3-mavenbuild'){
            steps{
                sh 'mvn package'
            }
        }
        stage('4-unittest'){
        steps{
            sh 'mvn test'
            }
        }
        stage('5-code-quality-check'){
            steps{
                mvn clean verify sonar:sonar \
  -Dsonar.projectKey=etech-scan \
  -Dsonar.host.url=http://3.80.1.193:9000 \
  -Dsonar.login=sqp_e28dc6c8c9f2fe87a0d6cddee2593bd2e5a34c12
            }
        }
    }
}