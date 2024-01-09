pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload')
        {
            steps
            {
                git 'http://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '4ba9a36c-6b0c-4856-a3a2-79207e94dce8', path: '', url: 'http://172.31.0.204:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContinousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '4ba9a36c-6b0c-4856-a3a2-79207e94dce8', path: '', url: 'http://172.31.7.254:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
