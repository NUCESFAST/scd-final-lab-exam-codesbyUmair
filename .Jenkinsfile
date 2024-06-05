pipeline {
    agent any

   /* environment {
        REGISTRY = 'your-docker-registry' // Replace with your Docker registry
        REPO_NAME = 'your-repo-name'      // Replace with your Docker repository name
        CREDENTIALS_ID = '7e8ef76f-dd7d-45f5-9996-71b2bcbeb21e' // Replace with your Jenkins Docker credentials ID
    }*/

    stages {
        stage('21i-1182-Clone Repository') {
            steps {
                git url: 'https://github.com/NUCESFAST/scd-final-lab-exam-codesbyUmair.git', branch: 'master'
            }
        }

        stage('21i-1182-Build and Push Docker Images') {
            parallel {
                stage('21i-1182-Build Auth Image') {
                    steps {
                        script {
                            dir('Auth') {
                                docker.build("${env.REGISTRY}/${env.REPO_NAME}-auth").push('latest')
                            }
                        }
                    }
                }
                stage('21i-1182-Build Classrooms Image') {
                    steps {
                        script {
                            dir('Classrooms') {
                                docker.build("${env.REGISTRY}/${env.REPO_NAME}-classrooms").push('latest')
                            }
                        }
                    }
                }
                stage('21i-1182-Build Client Image') {
                    steps {
                        script {
                            dir('client') {
                                docker.build("${env.REGISTRY}/${env.REPO_NAME}-client").push('latest')
                            }
                        }
                    }
                }
                stage('21i-1182-Build Event-Bus Image') {
                    steps {
                        script {
                            dir('event-bus') {
                                docker.build("${env.REGISTRY}/${env.REPO_NAME}-event-bus").push('latest')
                            }
                        }
                    }
                }
                stage('21i-1182-Build Post Image') {
                    steps {
                        script {
                            dir('Post') {
                                docker.build("${env.REGISTRY}/${env.REPO_NAME}-post").push('latest')
                            }
                        }
                    }
                }
            }
        }
    }

    post {
        always {
            echo '21i-1182-Cleaning up...'
            cleanWs()
        }
    }
}
