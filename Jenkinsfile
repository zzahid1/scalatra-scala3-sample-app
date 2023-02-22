// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            // Or, to avoid YAML:
            // containerTemplate {
            //     name 'shell'
            //     image 'ubuntu'
            //     command 'sleep'
            //     args 'infinity'
            // }
          yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: sbtscala/scala-sbt:eclipse-temurin-focal-11.0.17_8_1.8.2_2.13.10
    command:
    - sleep
    args:
    - infinity
''' 
            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'shell'
        }
    }
    stages {
        stage('java install'){
            steps('build'){
                //sh "su - && apt update -y && apt install -y default-jdk sbt"
                sh "echo hello"
            }
        }
        stage('SonarQube Analysis') {
            //def scannerHome = tool 'SonarScanner';
            steps('build 2'){
                withSonarQubeEnv('sonarqube') {
                    sh "sbt sonarScan"
                }
            }
  }
    }
}