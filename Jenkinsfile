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
      // bat '''
      // net use j: \\\\10.0.0.7\\Drops
      // dotnet nuget push bin/Debug/test-lib.1.0.0.nupkg -s j:/jenkins
      // '''
      cifsPublisher:
      cifsPublisher(publishers: [[transfers: [
         [
            // cleanRemote: true, 
            // excludes: '', 
            // flatten: false, 
            // makeEmptyDirs: false, 
            // noDefaultExcludes: false, 
            // patternSeparator: '', 
            // remoteDirectory: '', 
            // remoteDirectorySDF: false, 
            // removePrefix: '', 
            sourceFiles: 'bin/Debug/test-lib.1.0.0.nupkg'
         ]], 
         verbose: true]])
    }
  }
}