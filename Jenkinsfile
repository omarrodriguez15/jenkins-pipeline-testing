#!/usr/bin/env groovy
node {
  def nugetServer = 'j:/jenkins'

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
      cifsPublisher: 
         cifsPublisher(publishers: [
            [
               configName: 'local-drops', 
               transfers: [
                  [
                     sourceFiles: 'bin/Debug/test-lib.1.0.0.nupkg'
                  ]
               ], 
               verbose: true
            ]
         ])
    }
  }
}