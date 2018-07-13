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
    // Check for current route target
      ROUT_CHK = sh (
      script: """oc project jag-shuber-prod; oc get route sheriff-scheduling-reverse-proxy-prod -o template --template='{{ .spec.to.name }}' > route-target; cat route-target""")
      // echo ">> ROUT_CHK: ${ROUT_CHK}"

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
                url: "${currentBuild.absoluteUrl}/input"
              ],
              [
                type: "button",            
                text: "Deny",
                style: "primary",              
                url: "${currentBuild.absoluteUrl}/input"
              ]
            ])
        }
    }
  // Deploying to production
stage('Deploy to prod'){
    timeout(time:3, unit: 'DAYS'){ input id: 'TestProd', message: "Deploy to prod ${PROJECT_PREFIX}", submitter: 'kusingh6-admin', submitterParameter: 'approvingSubmitter' }
    node{
        // Checking current targeted route
        echo "Hello! This is just a test"
        }
    }


// // Functions to check currentTarget (api-blue)deployment and mark to for deployment to newTarget(api-green) & vice versa
  def getCurrentTarget() {
  def currentTarget = readFile("route-target")
  return currentTarget
  }

  def getNewTarget() {
  def currentTarget = getCurrentTarget()
  def newTarget = ""
  if (currentTarget == 'api-blue') {
      newTarget = 'api-green'
  } else if (currentTarget == 'api-green') {
      newTarget = 'api-blue'
  } else {
    echo "OOPS, wrong target"
  }
  return newTarget
  }