pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def targetPath = ""
                    
                    if (env.BRANCH_NAME == 'main') {
                        targetPath = "/var/www/html" 
                        echo "Deploying to PRODUCTION (Port 8081)"
                    } else if (env.BRANCH_NAME == 'dev') {
                        targetPath = "/var/www/dev_html" 
                        echo "Deploying to DEVELOPMENT (Port 8083)"
                    } else {
                        echo "Branch ${env.BRANCH_NAME} is not set for auto-deploy. Skipping."
                        return
                    }

                    sh "cp -f index.html ${targetPath}/index.html"
                    sh "echo 'DirectoryIndex index.html index.php' > ${targetPath}/.htaccess"
                    sh "chown www-data:www-data ${targetPath}/index.html ${targetPath}/.htaccess"
                }
            }
        }
    }
}
