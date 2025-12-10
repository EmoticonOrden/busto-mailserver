# Busto Mailserver
[Created for Docker Mailserver](https://github.com/docker-mailserver/docker-mailserver)
### How to deploy this
1. Clone or download this repository in chosen folder (or create folder for mailserver).
2. Replace all *PLACEHOLDERS* in compose.yaml and mailserver.env with your values.
3. Make folder "certs" in container folder and in it generate EC keys for encryption module through this command: `openssl ecparam -name prime256v1 -genkey | openssl pkey -out ecprivkey.pem | openssl pkey -in ecprivkey.pem -pubout -out ecpubkey.pem`
4. Generate cerificates for secure connections: `sudo certbot --apache/--nginx -d example.com` (replace example.com with your mail domain)
