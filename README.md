# nginx-template
Just some common templates that I used for my projects

## HTU
Replace domain.com with specific domain

## Match specific route
```
# Match exactly route
location = /specific-location{
    return 301 /another-location;
}
    
# Match all dynamic routes, this will match all routes such as /products/, /products/:id, etc
location ^~ /products/ {
    return 301 /another-location;
}
```

## Using Gzip
```
gzip on;
# gzip_static on;
gzip_min_length 10240;
gzip_comp_level 1;
gzip_vary on;
gzip_disable msie6;
gzip_proxied expired no-cache no-store private auth;
gzip_types
# text/html is always compressed by HttpGzipModule
text/css
text/javascript
text/xml
text/plain
text/x-component
application/javascript
application/x-javascript
application/json
application/xml
application/rss+xml
application/atom+xml
font/truetype
font/opentype
application/vnd.ms-fontobject
image/svg+xml;
```

## Caching static files
```
    location ~* \.(?:js|html|css|cur|jpe?g|gif|htc|ico|png|html|xml|otf|ttf|eot|woff|woff2|svg|webp)$ {
        expires 31536000;
        add_header Cache-Control public;

        # No need to bleed constant updates. Send the all shebang in on
        # fell swoop.
        tcp_nodelay off;

        # Set the OS file cache.
        open_file_cache max=3000 inactive=120s;
        open_file_cache_valid 45s;
        open_file_cache_min_uses 2;
        open_file_cache_errors off;

	    proxy_pass http://localhost:3000;
    }  
```
