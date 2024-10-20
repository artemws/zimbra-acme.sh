This addon for zimbra to get automaticly certificate from letsencrypt via acme.sh. All action you have to execute from root.

1. First of all, you have to install acme.sh and socat.
2. Let's create some dir, for example "/opt/certs" and setup chown "zimbra"
3. Put both sh scripts into "/opt/certs"
4. Edit deploy-zimbra-letsencrypt.sh and check domain and path for certs. Correct this parametrs for you.

```bash
#!/bin/bash
domain="mail.example.com"
certs=/opt/certs/
```
5. Setup chmod 755 for both scripts.

So, let's try to get our first certificate. Go into acme.sh directory and do it:
```bash
cd ~/.acme.sh
./acme.sh --set-default-ca  --server letsencrypt
./acme.sh --set-default-chain  --preferred-chain  ISRG  --server letsencrypt
./acme.sh -d mail.example.com --issue --standalone -k 2048 --pre-hook /opt/certs/zimbra-stop.sh --post-hook /opt/certs/deploy-zimbra-letsencrypt.sh
```
After this command, you will get and automaticly install certificate for your zimbra mail server. All renewal will be automaticly from crontab.
