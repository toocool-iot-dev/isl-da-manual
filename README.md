## General
The purpose of this document is to outline the Application Programming Interface (API) available via ISL metering hub platform. The web services allow accessing to data saved in the server with authorized users. This document provides information about the technical features of the API, and describes each API with its parameter formats and other related details. 

### Revision History
- December 2021 – first draft
- September 2022 – APIs’ details added
- October 2022 - Server installation manual added

## Introduction
The ISL API allows other software applications to access its device database for data query purposes, displaying device data in other applications, etc. The following is a list of available APIs:

API address: http://35.240.165.193:3000/v1

## Software Requirement for Server
1) Install MongoDB
    
    <https://www.mongodb.com/try/download/community>


2) Install MongoDB tool for restore database to local server machine

    <https://docs.mongodb.com/database-tools>

    - (For Windows) locate where this tool files are so we can execute the command.
    - Get latest backup database file <code>isl_data_ddmmyyyy.zip</code> (dd = date, mm = month, yyyy = year) from following link.
        
    <https://drive.google.com/file/d/1564_YAAC0UbGHG1ThiIlphtEPLQQpMG4/view?usp=sharing>
        
    - Unzip isl_data_ddmmyyyy.zip, this will unzip backup data into folder named <code>dump</code>.
    - From current directory <code>dump</code>, type command

            mongorestore

    This will restore database content from folder <code>dump</code> into current MongoDB server (local).

3) Install <strong>npm & Node.js</strong>

    <https://docs.npmjs.com/downloading-and-installing-node-js-and-npm>

4) Install <strong>yarn</strong>

    <https://classic.yarnpkg.com/en/>

## Source Code Installation

### For DATA Aggregator API Server

1) Pull source code from GitHub (use <code>clone</code> instead of <code>pull</code> for initializing git repo locally):

        git pull https://toocool-iot-dev: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@github.com/toocool-iot-dev/metering-hub.git  

    This git token will be monthly expired, for security purpose.
2) Get into directory.

        cd metering-hub

3) install javascript modules dependencies.
    
        yarn install

4) copy & paste this to .env file (create new file)

        ########### Beginning ############
        PORT=3003
        #MONGODB_URL=mongodb+srv://admin:impact007@meteringhub0.xw78d.mongodb.net/MeteringHub0?retryWrites=true&w=majority
        MONGODB_URL=mongodb://localhost:27017/metering_hub_0
        JWT_SECRET=thisisasamplesecret
        JWT_ACCESS_EXPIRATION_MINUTES=300
        JWT_REFRESH_EXPIRATION_DAYS=30
        # SMTP configuration options for the email service
        # For testing, you can use a fake SMTP service like Ethereal: https://ethereal.email/create
        SMTP_HOST="smtp.mailtrap.io"
        SMTP_PORT=2525
        SMTP_USERNAME="d5a72332b609dc"
        SMTP_PASSWORD="34cc9fc2e3c2bb"
        EMAIL_FROM=support@toocool.com
        ########### End file #############

5) run in development mode (lots of message will be printing in console for debugging)

        yarn dev

6) Or run in PRODUCTION mode    

        yarn start

7) Or run in docker (development mode)

        yarn docker:dev 

8) Or run in docker (production mode)

        yarn docker:prod

### Install Data Aggreator API Front-end
1) Pull source code from GitHub (use <code>clone</code> instead of <code>pull</code> for initializing git repo locally):

        git pull https://toocool-iot-dev:fVBNPPDPq6d1IYRJ4KEwARNL2wvNCi1tgTX7@github.com/toocool-iot-dev/isl-device-management.git 
    
This git token will be monthly expired, for security purpose.

2) Get into directory.

        cd isl-device-management
3) Install javascript module dependencies.

        npm install

4) Build 

        npm run build

5) Run (where <code>xxxx = PORT</code>, normally PORT=3000 is used)

        serve -s build -l xxxx & 
    
6) For local access, go to:
 
    <http://localhost:xxxx>

7) For public access via html, use server URL (or IP address) instead of <code>localhost</code>.

    <http://35.240.165.193:3000/>

## API Endpoints