#!/usr/bin/env groovy
node {
  def nugetServer = 'z:/jenkins'

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
      bat "dotnet nuget push bin/Debug/test-lib.1.0.0.nupkg -s ${nugetServer}"
    }
  }
}