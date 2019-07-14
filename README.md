# apache-php
![ff](https://img.shields.io/docker/build/zfarrugia/apache-php.svg)

PHP 7 Web Server runnning Apache

# Configuration

Get started by creating a `Dockerfile`:

```
FROM zfarrugia/apache-php
```

## Sendmail Config
To setup sendmail for PHP and configure the SMTP account settings. See [Msmtp](https://wiki.archlinux.org/index.php/Msmtp).
Add the following to the Dockerfile.

```
# Set up php sendmail config
RUN echo 'sendmail_path = "/usr/bin/msmtp -t"' >> /usr/local/etc/php/conf.d/php-sendmail.ini; \
    echo "# Set default values for all following accounts.  " >  /etc/msmtprc; \
    echo "defaults                                          " >> /etc/msmtprc; \
    echo "#auth           on                                " >> /etc/msmtprc; \
    echo "#tls            on                                " >> /etc/msmtprc; \
    echo "#tls_trust_file /etc/ssl/certs/ca-certificates.crt" >> /etc/msmtprc; \
    echo "logfile        ~/.msmtp.log                       " >> /etc/msmtprc; \
    echo "                                                  " >> /etc/msmtprc; \
    echo "# Default                                         " >> /etc/msmtprc; \
    echo "account        default                            " >> /etc/msmtprc; \
    echo "host           mail                               " >> /etc/msmtprc; \
    echo "#port           587                               " >> /etc/msmtprc; \
    chmod 600 /etc/msmtprc
