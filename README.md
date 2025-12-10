# Busto Mailserver
[Created for Docker Mailserver](https://github.com/docker-mailserver/docker-mailserver)
### How to deploy this
1. Clone or download this repository in chosen folder (or create folder for mailserver).
2. Make folder "certs" in container folder and in it generate EC keys for encryption module through this command: `openssl ecparam -name prime256v1 -genkey | openssl pkey -out ecprivkey.pem | openssl pkey -in ecprivkey.pem -pubout -out ecpubkey.pem`
