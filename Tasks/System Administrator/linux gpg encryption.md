We have confidential data that needs to be transferred to a remote location, so we need to encrypt that data.We also need to decrypt data we received from a remote location in order to understand its content.

On storage server in Stratos Datacenter we have private and public keys stored /home/*_key.asc. Use those keys to perform the following actions.

Encrypt /home/encrypt_me.txt to /home/encrypted_me.asc.

Decrypt /home/decrypt_me.asc to /home/decrypted_me.txt. (Passphrase for decryption and encryption is kodekloud).

```
gpg --import private_key.asc
gpg --import public_key.asc
gpg --list-public-keys
gpg --list-secret-keys
gpg -e -r kodekloud@kodekloud.com -o /home/encrypted_me.asc encrypt_me.txt 
gpg -d -o /home/decrypted_me.txt decrypt_me.asc
```
