pipeline{
    agent any
    tools {
        jdk 'java'
        maven 'maven'
    }
    // environment {
    //     APP_NAME = "devops-pipeline"
    //     RELEASE = "1.0.0"
    //     DOCKER_USER = "badrul11"
    //     DOCKER_PASS = 'dockerhub'
    //     IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
    //     IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    //     // JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")

    // }
    stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }

        }
    
        stage("Checkout from SCM"){
            steps {
                git branch: 'master', credentialsId: '' , url: 'https://github.com/badrul-devops/devops-pipeline'
            }

        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

        }

        stage("Test Application"){
            steps {
                sh "mvn test"
            }

        }
        
        // stage("Sonarqube Analysis") {
        //     steps {
        //         script {
        //             withSonarQubeEnv(credentialsId: 'sonar') {
        //                 sh "mvn sonar:sonar"
        //             }
        //         }
        //     }

        // }

        stage("Build & Push Docker Image") {
            steps {
                script {
			sh 'docker build -t badrul11/demo11 .'
                    // docker.withRegistry('',DOCKER_PASS) {
                    //     docker_image = docker.build "${IMAGE_NAME}"
                    }

                    // docker.withRegistry('',DOCKER_PASS) {
                    //     docker_image.push("${IMAGE_TAG}")
                    //     docker_image.push('latest')
                   // }
                }
            }

        }

        // stage("Trivy Scan") {
        //     steps {
        //         script {
		//    sh ('docker run -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image ${DOCKER_USER}/${IMAGE_NAME}:latest--no-progress --scanners vuln  --exit-code 0 --severity HIGH,CRITICAL --format table')
        //         }
        //     }

        // }

        // stage ('Cleanup Artifacts') {
        //     steps {
        //         script {
        //             sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
        //             sh "docker rmi ${IMAGE_NAME}:latest"
        //         }
        //     }
        // }
        // stage('Trigger ManifestUpdate'){
        //     steps{
        //         build job: 'ManifestUpdate'
        //     }
        // }
    //}
}
