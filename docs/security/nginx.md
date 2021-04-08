# Secure the nginx configuration

According to [this link](https://geekflare.com/nginx-webserver-security-hardening-guide/)

```nginx
server_tokens off

server {
    ssl_dhparam                 /certs-keys/dhparams.pem;
    ssl_prefer_server_ciphers   on;
    ssl_protocols               TLSv1.2;
    ssl_ciphers                 "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA HIGH !RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS";
    ssl_session_cache           shared:SSL:40m;
    ssl_session_timeout         4h;
    ssl_session_tickets         on;
    add_header                  Strict-Transport-Security "max-age=31536000" always;
    add_header                  X-Frame-Options "SAMEORIGIN";
    add_header                  X-XSS-Protection "1; mode=block";
}
```