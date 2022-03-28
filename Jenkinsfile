pipeline{
    agent any
    stages{
        stage('Build'){
          steps{
              sh '''
                 cd packages
                 zip -r demo-jenkins.zip demo-jenkins/
                 access_token=$(curl -X POST \
                 	$serverURL/oauth/token \
                 	-H 'Accept:application/json' -H 'Content-Type:application/x-www-form-urlencoded' \
                 	-d 'grant_type=password&username=$userID@gmail.com&password=$userPASS&client_id=TOROMartini&client_secret=TOROMartini' | jq -r .access_token)
                 curl -X POST \
                 	"$serverURL/esbapi/packages/upload?stateOnCreate=STARTED&replaceExisting=true" \
                 	-H "accept:application/json" -H "Content-Type:multipart/form-data" -F "file=@demo-jenkins.zip;type=application/x-zip-compressed" \
                 	-H "Authorization:Bearer $access_token"
                 '''
          }
        }
      }
    }
