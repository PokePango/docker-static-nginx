# Docker Static Nginx

docker-compose.yml example :
```
nginx-cv:
    build: ./static-nginx
    restart: unless-stopped
    volumes:
        - ./static-nginx/src:/var/www/html
    environment:
        - VIRTUAL_HOST=www.website.com, website.com
        - VIRTUAL_PORT=8080
        - LETSENCRYPT_HOST=www.website.com, website.com
        - LETSENCRYPT_EMAIL=contact@website.com
    ports:
        - 8080:8080
```

Environment variables are set to use jwilder/nginx-proxy along with Let's Encrypt.

It can be easily linked to a hugo website:

```
hugo:
    image: jojomi/hugo:latest
    restart: unless-stopped
    volumes:
        - ./hugo/src:/src
        - ./static-nginx/src:/output
    environment:
        - HUGO_WATCH=true
        - HUGO_THEME=ananke
        - HUGO_BASEURL=website.com
```