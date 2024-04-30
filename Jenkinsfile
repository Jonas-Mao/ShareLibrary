#!groovy

@Library('ShareLibrary') _

def tools = new org.devops.tools()

String workspace = "/var/lib/jenkins/workspace"

pipeline {
    agent any
    options {
        timestamps()  //日志会有时间
        skipDefaultCheckout()  //删除隐式checkout scm语句
        timeout(time: 1, unit: 'HOURS')  //流水线超时设置1h
    }

    stages {
        stage("GetCode"){ 
                timeout(time:5, unit:"MINUTES"){
                    script{
                        println('获取代码')
                        tools.PrintMes("获取代码",'green')                     
                    }
                }
            }

            stage("Build"){
                steps{
                     timeout(time:20, unit:"MINUTES"){
                        script{
                            println('应用打包')
                            tools.PrintMes("应用打包",'green')
                        }
                    }
                }
            }
        
            stage("CodeScan"){
                steps{
                    timeout(time:30, unit:"MINUTES"){
                        script{
                            print("代码扫描")
                            tools.PrintMes("代码扫描",'green')
                        }
                    }
                }
            }
        }

    post {
        always {
            script{
                println("always")
            }
        }

        success {
            script{
                currentBuild.description = "\n 构建成功!" 
            }
        }

        failure {
            script{
                currentBuild.description = "\n 构建失败!" 
            }
        }

        aborted {
            script{
                currentBuild.description = "\n 构建取消!" 
            }
        }
    }
}
