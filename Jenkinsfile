def gv

pipeline {
    agent {
        docker { image 'ubuntu:latest' }
    }
    parameters {
        booleanParam(name: 'executeTests', defaultValue: false, description: '')
    }
    
    stages {
        stagve("init") {
            steps {
                script {
                   gv = load "script.groovy" 
                }
            }
        }
        stage("setup node jenkins") {
            steps {
                script {
                    gv.setpNode()
                }
            }
        }
        stage("build") {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        stage("test") {
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }   
}

