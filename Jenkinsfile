pipeline{
    agent any
    stages{
        stage('Build '){
          steps{
              sh '''
                 cd packages
                 zip -r demo-jenkins.zip demo-jenkins/
                 access_token=$(curl -X POST \
                 	URL/oauth/token \
                 	-H 'Accept:application/json' -H 'Content-Type:application/x-www-form-urlencoded' \
                 	-d 'grant_type=password&username=ID&password=PASS&client_id=TOROMartini&client_secret=TOROMartini' | jq -r .access_token)
                 curl -X POST \
                 	"URL/esbapi/packages/upload?stateOnCreate=STARTED&replaceExisting=true" \
                 	-H "accept:application/json" -H "Content-Type:multipart/form-data" -F "file=@demo-jenkins.zip;type=application/x-zip-compressed" \
                 	-H "Authorization:Bearer $access_token"
                 '''
          }
        }
      }
    }
