def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/FeynmanFan/JenkinsDocker']]]);
	}
	stage('build'){
		docker.withRegistry('https://192.168.1.43:5000', 'docker-registry'){
			sh 'docker buildx create --name cbbspace'
			sh 'docker buildx use cbbspace'
			sh 'docker buildx build -t 192.168.1.43:5000/chrisbbehrens/simplednc:jenkinsfile --platform=linux/amd64/v2,linux/amd64/v3 - < dncgit.Dockerfile --push'
		}
	}
}
