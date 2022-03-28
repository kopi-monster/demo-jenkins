pipeline{
    agent any
    stages{
        stage('Build'){
          steps{
              sh '''
                 cd packages
                 zip -r demo-jenkins.zip demo-jenkins/
                 access_token=$(curl -X POST \
                 	https://toro282.us-east.toroserver.com/oauth/token \
                 	-H 'Accept:application/json' -H 'Content-Type:application/x-www-form-urlencoded' \
                 	-d 'grant_type=password&username=toro.jason.quinto@gmail.com&password=yS5Z@iX0IM$c&client_id=TOROMartini&client_secret=TOROMartini' | jq -r .access_token)
                 curl -X POST \
                 	"https://toro282.us-east.toroserver.com/esbapi/packages/upload?stateOnCreate=STARTED&replaceExisting=true" \
                 	-H "accept:application/json" -H "Content-Type:multipart/form-data" -F "file=@demo-jenkins.zip;type=application/x-zip-compressed" \
                 	-H "Authorization:Bearer $access_token"
                 '''
          }
        }
      }
    }
