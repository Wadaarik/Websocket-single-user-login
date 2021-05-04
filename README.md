# Enforcing a single web socket connection per user with Node.js, Socket.IO, and Redis

Based on mariotacke tutorial : https://medium.com/hackernoon/enforcing-a-single-web-socket-connection-per-user-with-node-js-socket-io-and-redis-65f9eb57f66a

## Install

### Nodejs
```
npm install
```
### Socket.IO
```
npm install socket.io
```
### Redis
Via Ubuntu
```
sudo add-apt-repository ppa:redislabs/redis
sudo apt-get update
sudo apt-get install redis
```

## Configure Redis

https://medium.com/@umutuluer/resolving-the-err-client-sent-auth-but-no-password-is-set-error-b81438d10843

1. Open the redis config file.
```
sudo nano /etc/redis/redis.conf
```

2. Uncomment the passphrase line and set new password
```
# requirepass yourpassword
```

3. Open terminal and connect redis-cli
```
redis-cli
```

4. Set passphrase
```
CONFIG SET requirepass "yourpassword"
```

5. Finally, you can test
```
AUTH yourpassword
```

6. Replace password in server\index.js
```
password: process.env.REDIS_PASS || 'yourpassword',
```

7. Replace password in redis.js
```
password: process.env.REDIS_PASS || 'yourpassword',
```


## Start Server & Web
```
redis-server
npm run start:server
npm run start:web
```
