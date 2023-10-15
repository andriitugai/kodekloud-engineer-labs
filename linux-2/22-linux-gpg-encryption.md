## Linux GPG Encryption

We have confidential data that needs to be transferred to a remote location, so we need to encrypt that data.We also need to decrypt data we received from a remote location in order to understand its content.



On <span style='color:cyan'>**storage server**</span> in Stratos Datacenter we have private and public keys stored at <span style='color:cyan'>**/home/*_key.asc**</span>. Use these keys to perform the following actions.


- Encrypt <span style='color:cyan'>**/home/encrypt_me.txt**</span> to <span style='color:cyan'>**/home/encrypted_me.asc**</span>.


- Decrypt <span style='color:cyan'>**/home/decrypt_me.asc**</span> to <span style='color:cyan'>**/home/decrypted_me.txt**</span>. (Passphrase for decryption and encryption is <span style='color:cyan'>**kodekloud**</span>).


- The user ID you can use is <span style='color:cyan'>**kodekloud@kodekloud.com**</span>.