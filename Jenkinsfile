pipeline {
    agent { label "slave-node" }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3.2"
        jdk "jdk11"
    }
parameters {
  string defaultValue: 'giturl', description: 'Repourl', name: 'https://github.com/mrashutoshmuduli/my-project.git'
  string defaultValue: 'Branch', description: 'Branch Name', name: 'main'
}
environment {
  giturl = "https://github.com/mrashutoshmuduli/my-project.git"
}
    stages {
        stage('Build') {
            steps {
                
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/mrashutoshmuduli/my-project.git'

                
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
