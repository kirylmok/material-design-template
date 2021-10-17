pipeline {
    agent {
        label 'slave'
    }

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        stage ('NPM installation') {
            steps {
                sh "npm install -g --save-dev clean-css"
                sh "npm install -g uglify-js"
            }
        }

        stage ('Compressing JS/CSS') {
            parallel {

                stage ('uglify-js') {
                    steps {
                        sh "cat www/js/* | uglifyjs -o www/js/min.js"
                    }
                }

                stage ('clean-css') {
                    steps {
                        sh "cat www/css/* | cleancss -o www/css/min.css"
                    }
                }
            }
        }

        stage ('Archiving results') {
            steps {
                sh "tar -czvf results.tar.gz .gitignore www/js www/css"
            }
        }
    }
}
