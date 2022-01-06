pipeline {
    agent any
    triggers { pollSCM('* * * * *')}

    stages {
        //Implicit check-out stage
        // stage('Checkout') {
        //     steps {
        //         git url: 'https://github.com/catalingm/jgsu-spring-petclinic.git', branch: 'main'
        //     }
        // }
        
        stage('Build') {
            steps {
                bat "./mvnw clean package"
                //bat "exit -1" //testing a result fast : 0 = success, -1 = failure
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
        // changed {
        //     emailext subject: "Job \'${JOB_NAME}\' (build ${BUILD_NUMBER}) ${currentBuild.result}",
        //     to: 'test@jenkins',
        //     recipientProviders: [upstreamDevelopers(), requestor()], 
        //     body: "Please go to ${BUILD_URL} and verify the build", 
        //     attachLog: true, 
        //     compressLog: true
        // }
    }
}
