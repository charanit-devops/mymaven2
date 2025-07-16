pipeline
{
    agent any
    stages{
        stage("ContinousDownload")
        {
            steps
            {
                git 'https://github.com/charanit-devops/maven.git'
            }
        }
        stage("ContinousBuild")
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage("ContinousDeployment")
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'fe277a7d-04ed-4965-87df-766eabd47721', path: '', url: 'http://172.31.80.136:8080')], contextPath: 'newtestapp', war: '**/*.war'
            }
        }
        stage("ContinousTesting")
        {
            steps
            {
                git 'https://github.com/charanit-devops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline/testing.jar'
            }
        }
        stage("ContinousDelivery")
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'fe277a7d-04ed-4965-87df-766eabd47721', path: '', url: 'http://172.31.84.208:8080')], contextPath: 'newprodapp', war: '**/*.war'
            }
        }
    }
}
