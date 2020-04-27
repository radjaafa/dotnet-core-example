pipeline {
    agent {
        label "WindowSlave"
    }
    stages {
        stage ('Checkout'){
            steps {
                git url: 'https://github.com/radjaafa/dotnet-core-example'
            }
        }
        stage ('Restore packages') {
            steps{
                bat "dotnet restore"
            }
        }
        stage ('Clean '){
            steps{
                bat 'dotnet clean'
            }
            
        } 
        stage('Build & SonarScanner'){
            steps{
                bat 'dotnet add tests/Conduit.IntegrationTests/ package coverlet.msbuild' 
                bat 'dotnet test tests/Conduit.IntegrationTests/Conduit.IntegrationTests.csproj /p:CollectCoverage=true /p:CoverletOutputFormat=opencover'
               /* --results-directory:C:/Jenkins/report --collect:"Code Coverage"*/
                bat 'dotnet sonarscanner begin /k:dotnetcore /d:sonar.host.url=http://35.184.124.47:9000/ /d:sonar.login=f83801e34a77001abefac3ddb2cb0946499c46dd /d:sonar.cs.opencover.reportsPaths="tests/Conduit.IntegrationTests/coverage.opencover.xml" /d:sonar.coverage.exclusions="**Tests*.cs"'
                bat 'dotnet build --configuration Release'
                bat 'dotnet sonarscanner end /d:sonar.login=admin /d:sonar.password=admin'

   
            }
        }
      /*  stage('Pusher'){
            steps{
                bat 'dotnet push /tests/Conduit.IntegrationTests/Conduit.IntegrationTests.csproj -c Release -o C:/Jenkins' +env.JOB_NAME+'/'+env.BUILD_NUMBER
            }
        } */
        stage('Pack'){
            steps{
               /* bat 'nuget pack tests/Conduit.IntegrationTests/*.csproj'*/
                bat 'dotnet pack tests/Conduit.IntegrationTests/'
                bat 'dotnet pack src/Conduit/'
            }
        }
    }
}
