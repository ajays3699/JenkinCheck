pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "AjayMaven"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
               // git 'https://github.com/ajays3699/check1.git'
                git branch: 'main', url: 'https://github.com/ajays3699/maven.git'

                // Run Maven on a Unix agent.
            //    sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                  //  junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'ajaysapp/target/*.war'
                    deploy adapters: [tomcat9(credentialsId: 'c0db2cf5-754a-465a-825c-df4a3259acb3', path: '', url: 'http://localhost:8080')], contextPath: 'ajaysapp', war: '**/*.war'
                }
            }
        }
    }
}
