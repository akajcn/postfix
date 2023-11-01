# postfix
To install mailutils:

# 1. run update repository

`sudo apt update`

# 2. Install **mailutils** package:

`sudo apt install mailutils`

# 3. Edit **/etc/postfix/main.cf** file:

  3.1. Change the following line:

**relayhost=**

to

**relayhost=[smtp.gmail.com]:587**

Add to end's file:

```smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl/sasl_passwd
smtp_tls_security_level = may
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
```

# 4. Create a **sasl_passwd** file

  4.1. sudo vim /etc/postfix/sasl/sasl_passwd

    4.1.1. Add to created file the following contents:

```[smtp.gmail.com]:587 EMAIL:PASSWORD```

4.1.2. Change the file's permission by security reasons:

`sudo chmod 600 /etc/postfix/sasl/sasl_passwd`

4.1.3. Encrypt the file:

`sudo postmap /etc/postfix/sasl/sasl_passwd`

4.1.4. Remove **/etc/postfix/sasl/sasl_passwd** file

`sudo rm -rf /etc/postfix/sasl/sasl_passwd` 

# 5. Restart postfix's service:

`service postfix restart`

# 6. Test the mail send:

`echo "mail send test | mail -s "Mail send test" akajcn@gmail.com < /dev/null`
