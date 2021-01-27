# Vue-Sails 

Email sender application 
- Sails as Backend 
- Vue as Frontend
- MySQL as database
- MailGun to send Email

Prarequesites:
- Make sure already have MailGun account and setup the authorized recipients
  https://help.mailgun.com/hc/en-us/articles/217531258


## Backend Sails

``` sails

- create database on mysql
- update config/datastores.js following your mysql settings
- update config/email, following your MailGun SMTP user and pass

# install dependencies
npm install

# run backend
sails lift

```

## Frontend Vue

``` bash

# install dependencies
npm install

# run frontend on port 8080
npm run serve

```


