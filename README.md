# Domain SSL Cloudflare Certificate Configure Steps

After hosting your app, follow the instructions below
## 1. Install Nginx
```
sudo apt install nginx
```
Go to this location
```
sudo nano /etc/nginx/sites-available/default
```
Add the following to the location part of the server block
```
        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                # try_files $uri $uri/ =404;

                proxy_pass http://localhost:5000; #whatever port your app runs on
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }
```
Check NGINX config error
```
sudo nginx -t
```
Restart NGINX
```
sudo service nginx restart
```
You should now be able to visit your IP with no port (port 80) and see your app. Now let's add a domain

## 2. Obtain Cloudflare SSL certificate and store it in the server
