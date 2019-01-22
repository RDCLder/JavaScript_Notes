# Storing Passwords

## General

- Hash-bashed message authentication code (HMAC)
  - Code that uses a cryptographic key alongside a hash function to store information
  - Provides the server and the client each with a private key
    - Known only to that specific server and that specific client
    - The client creates a unique HMAC (or hash) every time they make a request to the server
    - The request data is hashed with private keys and sent to the server
    - If the client's HMAC matches that of the server, then the request is accepted (called secret handshake)
  - More secure than message authentication code because both key and message are hashed in separate steps
  
- Dependencies
  - [pbkdf2](https://www.npmjs.com/package/pbkdf2)
    ```js
    npm installpbkdf2
    var pbkdf2 = require('pbkdf2')
    ```
  - [Crypto](https://nodejs.org/api/crypto.html)
    ```js
    crypto = require("crypto");
    ```

- Usage
  - Require dependencies and data to encrypt
    ```js
    var pbkdf2 = require('pbkdf2');
    var crytpo = require('crypto');
    var password = 'some-password'; // In this case, a password is being encrypted
    ```
  - Define the salt parameter
    - ```crypto.randomBytes(size)```
      - [Documentation](https://nodejs.org/api/crypto.html#crypto_crypto)
      - Generates cryptographically strong pseudo-random data
      - Size argument is a number indicating the number of bytes to generate
    ```js
    var salt = crypto.randomBytes(20).toString('hex');
    ```
  - Use an encryption algorithm
    ```js
    var key = pbkdf2.pbkdf2Sync(
      password, salt, 36000, 256, 'sha256'
    );
    ```
  - Hash the key
    ```js
    var hash = key.toString('hex');
    ```
  - Store data
    ```js
    var stored_pass = `pbkdf2_sha256$36000$${salt}$${hash}`;
    ```
    
- Creating and Storing Password
  - Take user password
  - Generate a salt and convert to string
  - Hash salt with user entered password using a cryptographic algorithm
  - Convert result to hexadecimal
  - Store result as password alongside salt parameters
  
- Compare password entry with stored password
  ```js
  var stored_pass = `pbkdf2_sha256$36000$${salt}$${hash}`;
  // checking a password
  var pass_parts = stored_pass.split('$');
  var key = pbkdf2.pbkdf2Sync(
    'some-password',
    pass_parts[2],
    parseInt(pass_parts[1]),
    256, 'sha256'
  );
  var hash = key.toString('hex');
  if (hash === pass_parts[3]) {
    console.log('Passwords Matched!');
  }
  ```
