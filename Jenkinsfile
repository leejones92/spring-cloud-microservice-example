stage 'Compile And Package'

node {
   git 'https://github.com/yunlzheng/spring-cloud-microservice-example.git'
   echo 'Run unit test'
   echo 'run compile'
}

stage 'Static Code Check'

node {
    echo 'run sonar runner'
}

stage 'Acceptence Test'

parallel 'integration-tests':{
    node{
        sh 'echo integration-tests'
    }
}, 'functional-tests':{
    node{
        sh 'echo functional-tests'
    }
}

stage 'Deploy To UAT'
input '发布到用户验收环境？'
echo "Deploy to UAT"

def next(build_num) {
	sh "echo current build number ${build_num}"
    build job: 'next_job', parameters: [[$class: 'StringParameterValue', name: 'UPSTREAM_BUILD_NUMBER', value: '$BUILD_NUMBER']]
}
