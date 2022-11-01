def gv

pipeline {
    agent none
 
    parameters {
        booleanParam(name: 'executeTests', defaultValue: false, description: '')
    }
    stages {
        stage("init") {
            agent { label "ubuntu-latest-node" }
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
            agent { label "ubuntu-latest-node" }
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        stage("test") {
            agent { label "ubuntu-latest-node" }
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
            agent { label "ubuntu-latest-node" }
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }   
}

