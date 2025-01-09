
@Library("Shared") _
pipeline {
    agent { label "vinod2" }

    stages {
        stage('Cloning') {
            steps {
                script {
                    clone("https://github.com/Vijay2359/new_todo.git", "main")
                }
            }
        }
        stage('Building') {
            steps {
                echo 'Building Docker image'
                script {
                    imgbuild("todo", "latest", "Vijay2359")
                }
            }
        }
        stage('Login into DockerHub') {
            steps {
                echo 'Logging into DockerHub'
                script {
                    push("todo","latest","vijay2359")
                }
            }
        }
        stage('Run a Container') {
            steps {
                echo 'Running Docker container using Docker Compose'
                sh "docker compose down && docker-compose up --build -d"

                // Use Docker exec to modify server.js and public/index.html inside the container
                sh """
                    docker exec cicd_app_1 sh -c "sed -i 's/localhost/3.83.126.230/' server.js"
                    docker exec cicd_app_1 sh -c "sed -i 's/localhost/3.83.126.230/' public/index.html"
                """
            }
        }
    }
}
