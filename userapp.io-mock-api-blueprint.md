FORMAT: 1A
HOST: http://127.0.0.1:3000

# Userapp.io Mock API
A simple mock api for [Userapp.io](https://userapp.io/) that mocks api responses. For offline local development, install api-mock (`npm -g install api-mock`) and run: 

    git clone https://gist.github.com/c0812bc687804b526a2b.git userappiomock
    api-mock userappiomock/userapp.io-mock-api-blueprint.md --port 3000 --cors-disable false
    
The local api is then available on http://localhost:3000/

To use it, make sure you have downloaded `https://app.userapp.io/js/userapp.client.js` and `https://app.userapp.io/js/angularjs.userapp.js` and include them, for instance:

    <!--
    <script src="https://app.userapp.io/js/userapp.client.js"></script>
    <script src="https://app.userapp.io/js/angularjs.userapp.js"></script>
    -->
    <script src="js/local-vendor/userapp.client.js"></script>
    <script src="js/local-vendor/angularjs.userapp.js"></script>

Then in `.run()`, override the userapp configuration to use the local mock api:

    user.init({ appId: 'fo123' });
    UserApp.setBaseAddress('127.0.0.1:3000');
    UserApp.setSecure(false);
    UserApp.setDebug(true);

All your sign-ups will act like they were successful but email needs to be verified. All logins will be successful (of course no email validation is necessary). The userapp id can be set to anything, it is completely ignored.

Mock API documentation is available on [http://docs.userappiomock.apiary.io/](http://docs.userappiomock.apiary.io/)

Happy offline dev :)

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

        [
          {
            "user_id": "a1a1a1a1a1a1a1a1a1a1a1",
            "first_name": "John Doe",
            "last_name": null,
            "email": "john.doe@example.com",
            "email_verified": true,
            "login": "john.doe@example.com",
            "properties": {},
            "features": {},
            "permissions": {},
            "subscription": null,
            "lock": null,
            "locks": [],
            "ip_address": "127.0.0.1",
            "last_login_at": 1421692047,
            "updated_at": 1421692047,
            "created_at": 1421691810
          }
        ]

## Token Heartbeat [/v1/token.heartbeat]
### Get user information [POST]
+ Request (application/json)

        null

+ Response 200 (application/json)

        {"alive":true}
