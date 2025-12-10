# Busto Mailserver
[Created for Docker Mailserver](https://github.com/docker-mailserver/docker-mailserver)
### How to deploy this
1. Make sure, you're installed Docker and Docker Compose.
2. Create the volumes described in `compose.yaml` or create volumes with your name and adjust the values ​​in `complose.yaml`.
3. Clone or download this repository in chosen folder (or create folder for mailserver).
4. Replace the following values:
   * *PLACEHOLDERS* in `compose.yaml` and `mailserver.env`. (for basic server operation)
   * For what suits you in `mailserver.env`. (advanced server configuration)
5. Make folder "certs" in container folder and in it generate EC keys for encryption module through this command: `openssl ecparam -name prime256v1 -genkey | openssl pkey -out ecprivkey.pem | openssl pkey -in ecprivkey.pem -pubout -out ecpubkey.pem`
6. Generate cerificates for secure connections: `sudo certbot --apache/--nginx/--certonly -d example.com` (replace example.com with your mail domain and use one of preffered options for certificate obtaining).
7. All set for first deploy, use `sudo docker-compose up -d` for the first run!
8. 
