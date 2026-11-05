#!/usr/bin/env groovy
@Library('jenkins-shared-library')
def gv

pipeline {
    agent any
    tools {
        maven 'maven-3.10'
    }
    stages {
        stage('init') {
            steps {
                script {
                    gv = load 'script.groovy'
                }
            }
        }

        stage('test') {
            steps {
                script {
                    echo "Running tests..."
                    echo "Executing pipeline on branch: ${BRANCH_NAME}"
                }
            }
        }

        stage('build jar') {
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage('build image') {
            steps {
                script {
                    buildImage()
                }
            }
        }

        stage('deploy') {
            when {
                expression { BRANCH_NAME == 'main' }
            }
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
