pipeline{
    agent any
    triggers{ pollSCM ('* * * * *') }
    parameters { choice (name: 'maven_goal', choices: ['package', 'install', 'deploy'], description: 'bulid with parametets')}
    stages{
        stage ('vcs'){
            steps{
                git branch: 'declaretive', url: 'https://github.com/anilreddy9100/spring-petclinic.git'
            }
        }
        stage ('packege'){
                tools {jdk 'JDK_17'
            }
            steps{
                sh "mvn ${params.maven_goal}"
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('SONAR_TOKEN') {
                sh 'mvn clean package sonar:sonar  -Dsonar.organization=anil12345  -Dsonar.projectKey=ANIL123456789 -Dsonar.projectName=ANIL123456789'
              } 
            }
        }
        
        stage ( 'postbuild' ){
            steps {
                archiveArtifacts artifacts: '**/spring-petclinic-*.jar',
                     onlyIfSuccessful: true 
                junit testResults : '**/TEST-*xml'     
            }
        }
    }
} 