instagram api call test
==========================

```bash
# launch callback server
python -m SimpleHTTPServer

# instagram authenticate
CLIENT_ID=<CLIENT_ID>
CLIENT_SECRET=<CLIENT_SECRET>
CALLBACK_URL=http://localhost:8000/callback.html

URL="https://www.instagram.com/oauth/authorize/?client_id=$CLIENT_ID&redirect_uri=$CALLBACK_URL&response_type=code"

# open (redirect to callback_url)
open $URL

# get access token
CODE=<CODE>

curl -F "client_id=$CLIENT_ID" \
-F "client_secret=$CLIENT_SECRET" \
-F "grant_type=authorization_code" \
-F "redirect_uri=$CALLBACK_URL" \
-F "code=$CODE" \
https://api.instagram.com/oauth/access_token

# call instagram api
ACCESS_TOKEN=<access token>

curl https://api.instagram.com/v1/users/self/?access_token=$ACESS_TOKEN | jq .
{
  "meta": {
    "code": 200
  },
  "data": {
    "username": "046k2m",
    "bio": "",
    "website": "",
    "profile_picture": "https://igcdn-photos-h-a.akamaihd.net/hphotos-ak-xpt1/t51.2885-19/s150x150/11881588_840842726011359_1932449395_a.jpg",
    "full_name": "",
    "counts": {
      "media": 145,
      "followed_by": 38,
      "follows": 38
    },
    "id": "38139220"
  }
}
```
