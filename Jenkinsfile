pipeline{
    agent any
    triggers{ pollScm ('* * * * *') }
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
    }
}