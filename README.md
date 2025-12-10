# Busto Mailserver
Just **ready-to-use** configuration, no more. [Created for Docker Mailserver.](https://github.com/docker-mailserver/docker-mailserver) 
## What you need?
* Your domain
* Docker and Docker Compose
* External IP address, exposed to the Internet
## What can it do?
* A low-resource mail server.
* Your configuration, mailboxes and the letters themselves stores in Docker volumes, you can find this in `/var/lib/docker/volumes` and backup/restore easily!
## How to deploy this
1. Make sure, you're installed Docker and Docker Compose.
2. Create the volumes described in `compose.yaml` or create volumes with your name and adjust the values ​​in `compose.yaml`.
3. Clone or download this repository in chosen folder. (or create folder for mailserver)
4. Replace the following values:
   * *PLACEHOLDERS* in `compose.yaml` and `mailserver.env`. (for basic server operation)
   * For what suits you in `mailserver.env`. (advanced server configuration)
5. Make folder "certs" in container folder and in it generate EC keys for encryption module through this command: `openssl ecparam -name prime256v1 -genkey | openssl pkey -out ecprivkey.pem | openssl pkey -in ecprivkey.pem -pubout -out ecpubkey.pem`.
6. Generate cerificates for secure connections: `sudo certbot --apache/--nginx/--certonly -d example.com`. (replace example.com with your mail domain and use one of preffered options for certificate obtaining)
7. Make `dkim` folder in container folder.
8. All set for first deploy, use `sudo docker-compose up -d` for the first run!
9. But I think you want emails to reach their senders, right? So now we need to configure the DKIM. For this we need make folder in container for DKIM or mount folder in `compose.yaml`. (already mounted)
10. In container, in `/etc/rspamd/dkim`, use this command for creation DKIM key pairs, `rspamadm dkim_keygen -s mail -d example.com -k mail.key` and copy or remember line like this `mail._domainkey IN TXT ( "v=DKIM1; k=rsa;" "p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDTwN..."`. (after `p=...` is written your key for DKIM)
11. After this, set some file permissions: `sudo chown -R _rspamd:_rspamd /etc/rspamd/dkim/ && sudo chmod 600 /etc/rspamd/dkim/*.key`.
12. Modify your DNS with next record: `mail._domainkey.example.com. IN TXT "v=DKIM1; k=rsa; p=...*YOUR_GENERATED_KEY*"` and submit this to your DNS. (replace example.com with your domain)
13. Shutdown your container with `sudo docker-compose down`.
14. Find and modify `example.com` in your `dkim_signing.conf` and replace with your domain.
15. Restart your container with `sudo docker-compose up -d`.

**And your mail server is ready to go! Congratulations!**
You can deeply modify this server later, if you want.

## Known issues
Full-Text Search may not work or may give errors while running. I haven't been able to resolve this yet :(
