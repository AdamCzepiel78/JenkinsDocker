def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/FeynmanFan/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('chrisbbehrens/agent-dnc:v' + env.BUILD_NUMBER, './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('https://192.168.1.43:5000', 'docker-registry'){
			dockerImage.push();
		}
	}
}
