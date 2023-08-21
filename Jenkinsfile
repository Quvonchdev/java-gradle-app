pipeline{
    agent any
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages{
        stage("Clon code"){
            steps {
                echo "Cloneing the code"
                git url:"https://github.com/Quvonchdev/gradle-app.git", branch: "main"
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
                            docker lohin -u quvonchdev -p $docker_password localhost:4000
                            docker push localhost:4000/springapp:${VERSION}
                            docker rmi localhost:4000/springapp:${VERSION}
                        '''
                    }
                    
                }
            }
        }
    }
}