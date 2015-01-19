FORMAT: 1A

# userappiomock
A simple mock api for [Userapp.io](https://userapp.io/) that mocks api responses. To use during testing. For offline local development, install api-mock (`npm -g install api-mock`) and run: 

    wget 
    api-mock $@ --port 3000
    
The local api is then available on https://localhost:3000/

# Group V1
Resources corresponding to version 1 of the Userapp.io API

## User Save [/v1/user.save]
### Sign-up [POST]
+ Request (application/json)

        {"first_name":"John Doe","login":"john.doe@example.com","email":"john.doe@example.com","password":"pass123"}

+ Response 200 (application/json)

        {"user_id":"a1a1a1a1a1a1a1a1a1a1a1","first_name":"John Doe","last_name":null,"email":"john.doe@example.com","email_verified":false,"login":"john.doe@example.com","properties":{},"features":{},"permissions":{},"subscription":null,"lock":null,"locks":[{"type":"EMAIL_NOT_VERIFIED","reason":"Email requires verification.","issued_by_user_id":"b1b1b1b1b1b1b1b1b1b1b1","created_at":1421691810}],"ip_address":"127.0.0.1","last_login_at":0,"updated_at":1421691810,"created_at":1421691810}

## User Login [/v1/user.login]
### Log in [POST]
+ Request (application/json)

        {"login":"john.doe@example.com","password":"pass123"}

+ Response 200 (application/json)

        {"token":"t1t1t1t1t1t1t1t1t1t1t1","user_id":"a1a1a1a1a1a1a1a1a1a1a1","lock_type":null,"locks":[]}

## User Get [/v1/user.get]
### Get user information [POST]
+ Request (application/json)

        {"user_id":"self"}

+ Response 200 (application/json)

        [{"user_id":"a1a1a1a1a1a1a1a1a1a1a1","first_name":"John Doe","last_name":null,"email":"john.doe@example.com","email_verified":true,"login":"john.doe@example.com","properties":{},"features":{},"permissions":{},"subscription":null,"lock":null,"locks":[],"ip_address":"127.0.0.1","last_login_at":1421692047,"updated_at":1421692047,"created_at":1421691810}]

## Token Heartbeat [/v1/token.heartbeat]
### Get user information [POST]
+ Request (application/json)

        null

+ Response 200 (application/json)

        {"alive":true}

