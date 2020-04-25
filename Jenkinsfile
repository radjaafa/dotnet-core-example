pipeline {
    
    environment {
        GIT_REPO = "https://github.com/radjaafa/dotnet-core-example"
    }
    agent {
        label "WindowSlave"
    }
    stages {
        stage ('Checkout'){
            steps {
                git credentialsId:'radjaafa', url: "${GIT_REPO}", branch:'master'
            }
        }
        stage ('Clean'){
            steps{
                bat 'dotnet clean'
            }
            
        } 
        stage('Build'){
            steps{
                bat 'dotnet build --configuration Release'
            }
        }
        stage('Pack'){
            steps{
                bat 'dotnet pack --no-build --output nupkgs'
            }
        }
      /*  stage('Push'){
            steps{
                bat "dotnet nuget push **\\nupkgs\\*.nupkg -k hereisapikey"
            }
        }*/
        stage ('test'){
            steps{
                dotnet 'add package coverlet.msbuild'
                dotnet 'test tests/Conduit.IntegrationTests/Conduit.IntegrationTests.csproj /p:CollectCoverage=true'
            }
        }
       /* stage('codeCover'){
            steps{
                powershell.exe -NoProfile -ExecutionPolicy Bypass ./TestsAndCoverage.ps1
            }
        }*/
    }
}
