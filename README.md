# Spika

Spika is messenger module for Web/iOS/Android with backend. 
You can include messenger feature to your app or service with minimum code.

For detail please visit our web site.
http://spikaapp.com

![Demo](https://github.com/cloverstudio/Spika/blob/master/spika_demo_new.gif "Demo")

Instruction for each device you can see here.

## Backend

https://github.com/cloverstudio/Spika/tree/master/web/src/server

## Web Client

https://github.com/cloverstudio/Spika/tree/master/web/src/client

## Android

https://github.com/cloverstudio/Spika/tree/master/Android

## iOS

https://github.com/cloverstudio/Spika/tree/master/iOS


## License

MIT License


Setting Up Server
Here is step by step instruction to setup new backend and frontend. Before doing this all our clients have to buy license and we provice access permission to our github private repository.

Minimum server requirements.
This tutorial is done using t2.micro instance in Amazon Web Service using Ubunti 16.04. t2.micro instance's spec is following.

CPU	1core 1GHz
Memory	1GB
Storage	8GB
Please be careful it is minimum server requirements, you will need more powerful server for production or even for development.

Setting up backend.
Install softwares
$ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
$ sudo apt-get install -y nodejs
$ sudo apt-get install -y git imagemagick build-essential libfuse-dev libcurl4-openssl-dev libxml2-dev mime-support automake libtool mongodb redis-server turnserver python
Clone from repository
You will have your own repository. So please change this url part.

$ git clone https://github.com/cloverstudio/SFB_Server.git
Setup Backend
$ cd SFB_Server
$ npm install
Start servers
$ sudo /etc/init.d/mongodb start
$ sudo /etc/init.d/redis-server start
Edit init.js
$ cp src/server/lib/init-sample.js src/server/lib/init.js
$ vim src/server/lib/init.js
Probably you have to change following configuration to start server.

Config.port = 8080; 
Please be sure the port is opened so you can access to the server from browser.

Create directory
$ mkdir public/uploads
Start Spika Backend
$ sudo node src/server/main
If you see this Spika is correctly started.

Connecting mongoDB mongodb://localhost/spikaenterprise
Server listening on port 8080!
In some cases following error could occure.
Error: Cannot find module '../build/Debug/iconv.node'
    at Function.Module._resolveFilename (module.js:469:15)
If you encount this error please just do this.

$ npm i iconv
What's next ?
Please open service owner admin console like this

http://54.215.140.61:8080/owner
Put Username and Password which is in init.js


Setting Turn/Stun server
Spika uses standard turn-stun protocol for WebRTC communication.

We recommend to user this server to host Turn/Stun by your self. https://github.com/coturn/coturn

Install library
$ wget https://github.com/downloads/libevent/libevent/libevent-2.0.21-stable.tar.gz
$ tar xvfz libevent-2.0.21-stable.tar.gz
$ cd libevent-2.0.21-stable
$ ./configure
$ make
$ sudo make install
Coturn installation
Find latest code from here. https://github.com/coturn/coturn/wiki/Downloads

Build

$ tar xvfz turnserver-<...>.tar.gz
$ ./configure
$ make
$ sudo make install
Start server

$ turnserver -L <public_ip_address> -o -a -f -r <realm-name>
You have detaild instructions here. https://github.com/coturn/coturn/wiki/CoturnConfig


Configuration
Here is explanation of init.js.

Config.host : Keep this "localhost"

Config.port : Runnning port.

Config.urlPrefix : Change this if you want change baseURL of API.

Config.dbCollectionPrefix : Im most case keep this empty string.

Config.databaseUrl : Connection string to mongoDB

Config.supportUserId : If you set userId here, the user appears to all users member list.

Config.forceLogoutAllDevice : Set true, if you want users to auto logout from all device when user logout from one device.

Config.redis : Connection info for Redis

Config.AESPassword : Password for encryption text message.

Config.publicPath : Where you put index.html and all sets for frontend part.

Config.uploadPath : Where saved files which users upload.

Config.socketNameSpace : Keep this as it is.

Config.defaultAvatar : Default avatar for users.

Config.defaultAvatarGroup : Default avatar for groups.

Config.hashSalt : Hash salt for generating hash from password.

Config.username : Service owner username.

Config.password : Service owner password.

Config.signinBackDoorSecret : This is used only for debugging purpose.

Config.apnsCertificates : Certificates for push notification.

Config.gcmAPIKey : This is depricated.

Config.fcmServerKey : FCM settings.

Config.webRTCConfig : WebRTC settings.

Config.email : Config.smtp : It is used for send email when user signup.

Config.protocol : If you use builtin ssl change here to "https://"

Config.twilio : It is used when you want allow users signup by telephone number.

Config.useVoipPush : Keep here true when you want use VoIP push for APN.

Config.useCluster : This is experimented parameter. We will announce when it wors correctly.

Config.robotUserId : Create user who you want use for webhooks.


Build instructions
Here is step by step instruction to setup development environment of frontend. Before doing this all our clients have to buy license and we provice access permission to our github private repository.

Clone from repository
You will have your own repository. So please change this url part.

$ git clone https://github.com/cloverstudio/SFB_Server.git
Install libraries
$ cd SFB_Serve
$ npm install
Edit config file
$ cp src/client/js/lib/init-sample.js src/client2/js/lib/config.js 
$ vim  src/client/js/lib/config.js
In production you will need only change these configurations.

hashSalt: "",
AESPassword: ""
Debug frontend
$ npm start
Then you can debug frontend by opening http://localhost:3000

Build source code
$ npm run build


