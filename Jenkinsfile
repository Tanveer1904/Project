pipeline
{
  agentany
  stages
  {
    stage('Contdownload')
    {
      steps
      {
        git 'https://github.com/Tanveer1904/Project.git'
      }    
    }
    stage('Build')
    {
      steps
      {
        sh 'docker build -f vote/Dockerfile -t Tanveer1904/votingapp vote/.'
        sh 'docker build -f result/Dockerfile -t Tanveer1904/resultapp result/.'
	sh 'docker build -f worker/Dockerfile -t Tanveer1904/workerapp worker/.'      }
    }
    stage('Push')
    {
      steps
      {
        sh 'docker push tanveer1904/votingapp'
	sh 'docker push tanveer1904/resultapp'
	sh 'docker push tanveer1904/worker'
      }
    }
    stage('Deploy')
    {
      steps
      {
        sh 'ssh ubuntu@ansibleip ansible-playbook /home/ubuntu/app.yml -b'
      }
    }
    stage('Testing')
    {
      steps
      {
        git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
	sh 'java -jar location/testing.jar'
      }
    }
    stage('Delivery')
    {
      steps
      {
        sh 'ssh ec2-user@ip kubectl apply -f /home/ec2-user/voting/k8s-specifications'
      }
    }
  }
}

