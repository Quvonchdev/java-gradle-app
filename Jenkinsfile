pipeline{
    agent any
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages{
        stage("Clon code"){
            steps {
                echo "Cloneing the code"
                git url:"https://github.com/Quvonchdev/java-gradle-app.git", branch: "main"
            }
        }
        // stage("soner quality chek"){
        //     agent {
        //         docker {
        //             image 'openjdk:11'
        //         }
        //     }
        //     steps{
        //         script{
        //             withSonarQubeEnv(credentialsId: 'sonar-token') {
        //                 sh 'chmod +x gradlew'
        //                 sh './gradlew sonarqube'
        //             }

        //         }
        //     }

        // }
        
        stage("docker build & docker push"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_password')]) {
                        sh '''
                            docker build -t localhost:4000/springapp:${VERSION} .
                            echo docker_password | docker login -u quvonchdev --password-stdin localhost:4000
                            docker push localhost:4000/springapp:${VERSION}
                            docker rmi localhost:4000/springapp:${VERSION}
                        '''
                    }
                    
                }
            }
        }
    }
}
