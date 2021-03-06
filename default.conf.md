# default.conf

``` bash
server {
    listen      80 default;
    server_name _;
    root        /var/www/vhosts/i-abc123;
    index       index.html index.htm;
    charset     utf-8;

    return 301 https://$host$request_uri;

    access_log  /var/log/nginx/i-abc123.access.log  main;
    error_log   /var/log/nginx/i-abc123.error.log;

    include     /etc/nginx/drop;

    add_header X-Cache-Status $upstream_cache_status;
    expires $expires;

    set $mobile '';
    #include /etc/nginx/mobile-detect;

    include     /etc/nginx/wp-front;

    #
    # When you use phpMyAdmin, uncomment the line "include /etc/nginx/phpmyadmin;"
    # and delete or comment out the below line "location ~* /(phpmyadmin|myadmin|pma) { }".
    #
    include     /etc/nginx/phpmyadmin;
    #location ~* /(phpmyadmin|myadmin|pma) { access_log off; return 404; }

    #
    # redirect server error pages to the static page /50x.html
    #
    error_page  502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```
