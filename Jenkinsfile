pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven-3') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven-3') {
                    sh 'mvn test'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'jenkins-example', 
                            classifier: '', 
                            file: '/var/lib/jenkins/workspace/Jenkins-Pipeline/target/Jenkins-Pipeline.jar', 
                            type: 'jar'
                        ]
                    ], 
                    credentialsId: 'nexus-user-credentials', 
                    groupId: 'com.techprimers.testing', 
                    nexusUrl: 'heeng-aawachar.headquarters.healthedge.com:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'heeng-aawachar.headquarters.healthedge.com:8081/repository/maven-nexus-repo/', 
                    version: '1.0.1'
                }
            }
        }
    }
