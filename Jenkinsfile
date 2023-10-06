pipeline{
    environment{
        dockerimagename = "guestdev/jenkins_demo"
        dockerImage = ""
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')

    }
    agent any
        stages{
            stage('clone'){
                steps{
                    git branch: 'master', credentialsId: 'github', url: 'https://github.com/manotisehgall/Jenkins_demo.git'
                }
            }

            stage('Build image'){
                steps{
                    script{
                        dockerImage = docker.build dockerimagename
                    }
                }

            }

            stage("Dockerhub login"){
                steps{
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }

            stage("Pushing image"){
                steps{
                    script{
                        dockerImage.tag("latest")
                        dockerImage.push("latest")
                    }
                }

            }
        }
}

