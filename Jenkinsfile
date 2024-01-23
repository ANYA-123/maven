pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload_master')
        {
            steps
            {
                git 'http://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinousBuild_master')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinousDeployment_master')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '4ba9a36c-6b0c-4856-a3a2-79207e94dce8', path: '', url: 'http://172.31.0.204:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContinousTesting_master')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinousDelivery_master')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '4ba9a36c-6b0c-4856-a3a2-79207e94dce8', path: '', url: 'http://172.31.7.254:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
