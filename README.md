# Get unencrypted credentials from google-chrome
    Script prints saved credentials in google-chrome(url, username, password)
##  Testing
    Tested on linux ubuntu 24.04.1, google-chrome(131.0.6778.204), google password manager
## Source code
    99% from https://github.com/priyankchheda/chrome_password_grabber
    I added only some debugging entries, comments
## How it works in linux
    * google-chrome stores url,username,passwords in sqlite db, in file "/home/coudek/.config/google-chrome/Default/Login Data"
    * Saved credentials are in table logins, url and username are unencrypted but password is encrypted
    * Secret values(passwords) are encrypted by cypher AES-128 CBC
    * Decryption/Encryption key for AES-128 CBC is derived from master password with using PBKDF2 with these params
        * salt is 'saltysalt'
        * key length is 16 bytes
        * init vector is 16 bytes of space character
        * number of iteration == 1
    * Master password is stored in gnome-keyring(kwallet), if not it is word 'peanuts'
## Notes
    * Linux chromium source code with ciphering details https://source.chromium.org/chromium/chromium/src/+/main:components/os_crypt/sync/os_crypt_linux.cc;bpv=0;bpt=1
    * 
