@Library('devops-library') _

def SLACK_PROD_CHANNEL="sheriff_prod_approval"
def SLACK_MAIN_CHANNEL="#sheriff_scheduling"

stage('Approval notification'){
  node{
      try{
            slackNotify(
            "New Version in environment 🚀",
            "A new version of the APP_NAME is now in environment",
            'good',
            env.PROD_SLACK_HOOK,
            SLACK_PROD_CHANNEL,
            [
              [
                type: "button",
                text: "View New Version",         
                url: "${url}"
              ],
              [
                type: "button",            
                text: "Deploy to Test?",
                style: "primary",              
                url: "${currentBuild.absoluteUrl}/input"
              ]
            ])
        }catch(error)
        {
          echo "error in build"
        }
        }
    }
  // Deploying to production
stage('Deploy to prod'){
    timeout(time:3, unit: 'DAYS'){ input "Deploy to prod"}
    node{
        // Checking current targeted route
        echo "Hello! This is just a test"
        }
    }
