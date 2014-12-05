devuan.fr
=========

French translation of devuan.org


Doc
---

* apt-get install markdown
* La page index est au format markdown dans views/index.html
* Pour générer le rendu : 
```
# ./webnomad/render
[*] WebNomad v0.5 running on GNU/Linux
[*] Rendering your website
 .  Title:  Devuan - GNU/Linux par des admins vétérans d'UNIX
 .  SYS = /srv/sites/www.devuan.fr/webnomad
 .  WEB_ROOT =
[*] Indexing custom fonts
 .  1 custom fonts indexed
 .  Clean up all temp files ... done
 .  Html rendering:  /srv/sites/www.devuan.fr/pub/index.html  .  1 markdown fields  .  done
 .  publishing all  views  ... done
[*] Website refreshed.
```

Config Nginx
------------
```
server {
        server_name www.devuan.fr;
        root /srv/sites/www.devuan.fr/pub;

        index index.htm index.html;
        etag off;

        location / {
                try_files $uri $uri/ /index.php?q=$uri&$args;
        }

        location ~* \.(txt|js|css|png|jpg|jpeg|gif|ico|svg)$ {
                expires 10d;
                log_not_found off;
        }

        access_log /var/log/nginx/devuan_access.log;
}
server {
        server_name  devuan.fr;
        return       301 http://www.devuan.fr$request_uri;
}
```
