#!/usr/bin/env groovy

node {
  stage('compile') {
    checkout scm
    dir('.') {
      bat 'dotnet restore'
      bat "dotnet build --version-suffix ${env.BUILD_NUMBER}"
    }
  }
}