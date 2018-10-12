#!/usr/bin/env groovy

node {
  stage('compile') {
    checkout scm
    dir('.') {
      bat 'dotnet restore'
      bat "dotnet build --version-suffix ${env.BUILD_NUMBER}"
    }
  }
  stage('compile') {
    checkout scm
    dir('test-lib') {
      bat 'dotnet pack test-lib.csproj'
      bat "dotnet nuget push bin/Debug/test-lib.1.0.0.nupkg -s z:/jenkins"
    }
  }
}