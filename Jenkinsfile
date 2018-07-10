@Library('devops-library') _

// Edit your app's name below
def APP_NAME = 'frontend'
def FRONTEND_B = 'frontend-blue'
def FRONTEND_G = 'frontend-green'
def API_B = 'api-blue'
def API_G = 'api-green'
def PATHFINDER_URL = "pathfinder.gov.bc.ca"
def PROJECT_PREFIX = "jag-shuber"
// Edit your environment TAG names below
def TAG_NAMES = [
  'prod'
]
def APP_URLS = [
  "https://${APP_NAME}-${PROJECT_PREFIX}-${TAG_NAMES[0]}.${PATHFINDER_URL}"
]

def SLACK_PROD_CHANNEL="sheriff_prod_approval"
def SLACK_MAIN_CHANNEL="#sheriff_scheduling"

stage('Approval notification'){
  node{
            slackNotify(
            "To Deploy Blue stack with prod tagged image 🚀",
            "To switch to new version",
            'Please Aproove or Deny!!',
            env.PROD_SLACK_HOOK,
            SLACK_PROD_CHANNEL,
            [
              [
                type: "button",
                text: "Approve",         
                url: "${currentBuild.absoluteUrl}/input/d1e7302f6cd48cc7aecd670c062b1f11/Proceed"
              ],
              [
                type: "button",            
                text: "Deny",
                style: "primary",              
                url: "${currentBuild.absoluteUrl}/wfapi/inputSubmit?inputId=Abort"
              ]
            ])
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
