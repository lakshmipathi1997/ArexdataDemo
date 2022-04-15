pipeline
{
	stages
	{
		stage('Build')
		{
			steps
			{
				echo "Build is Started"
				bat "mvn clean package -PRegression -DskipTests=true"
				echo "Build is Successful"
			}
		}
		stage('Smoke TestSuite')
		{
			parallel
			{
				stage('Chrome')
				{
					steps
					{
						echo "Smoke Test Execution is Started in Chrome"
						bat "mvn test -PSmoke -Dbrowser=Chrome"
						echo "Smoke Test Execution is Successful in Chrome"
					}
				}
				stage('Firefox')
				{
					steps
					{
						echo "Smoke Test Execution is Started in Firefox"
						bat "mvn test -PSmoke -DskipTests=true"
						echo "Smoke Test Execution is Successful in Firefox"
					}
				}
			}
		}
		stage('Regression TestSuite')
		{
			parallel
			{
				stage('Chrome')
				{
					steps
					{
						echo "Regression Test Execution is Started in Chrome"
						bat "mvn test -PRegression -DBrowser=Chrome"
						echo "Regression Test Execution is Successful in Chrome"
					}
				}
				stage('Firefox')
				{
					steps
					{
						echo "Regression Test Execution is Started in Firefox"
						bat "mvn test -PRegression -DskipTests=true"
						echo "Regression Test Execution is Successful in Firefox"
					}
				}
			}
		}
		stage('Publish Reports')
		{
				stage('Extent Report')
				{
					steps
					{
						publishHTML([
						allowMissing: false, 
            					alwaysLinkToLastBuild: true, 
            					keepAll: false, 
						reportDir: 'test-output', 
            					reportFiles: 'Smoke Test', 
            					reportName: 'Suite1', 
            					reportTitles: ''])
					}
				}
			}
				stage('Gmail')
				{
					steps
					{
						emailext body: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}",
						subject: 'Test Automation Pipeline Build Status',
						to: 'lakshmipathimunna@gmail.com'
					}
				}
	post
	{
		failure 
		{
            		echo 'This Job is Failed - Notifications have been sent to Gmail..!!'	
			emailext body: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}",
			subject: 'Test Automation Pipeline Build Status',
			to: 'lakshmipathimunna@gmail.com'
		}
        	unstable 
		{
           		echo 'This Job is Unstable - Notifications have been sent to  Gmail..!!'    		
			emailext body: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}",
			subject: 'Test Automation Pipeline Build Status',
			to: 'lakshmipathimunna@gmail.com'
		}
	}
}