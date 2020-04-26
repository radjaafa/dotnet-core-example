pipeline {
    agent {
        label "WindowSlave"
    }
    environment {
        dotnet = 'C:\Program Files\dotnet'
    }
    stages {
        stage ('Checkout'){
            steps {
                git credentialsId:'radjaafa', url: 'https://github.com/radjaafa/dotnet-core-example', branch:'master'
            }
        }
