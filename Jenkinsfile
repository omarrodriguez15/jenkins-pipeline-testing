#!/usr/bin/env groovy
node {
  def buildArtifact = "build-artifact-${env.BUILD_NUMBER}.zip"

  stage('compile') {
    checkout scm
    dir('.') {
      bat 'dotnet restore'
      bat "dotnet build "
    }
  }
  stage('nuget-creation') {
    checkout scm
    dir('test-lib') {
      bat 'dotnet pack test-lib.csproj'
      zip zipFile: buildArtifact, dir: "bin/Debug/"
      archiveArtifacts artifacts: buildArtifact, fingerprint: true
      cifsPublisher: 
         cifsPublisher(publishers: [
            [
               configName: 'local-drops', 
               transfers: [
                  [
                     sourceFiles: buildArtifact
                  ]
               ], 
               verbose: true
            ]
         ])
    }
  }
}