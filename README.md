# Tunneling

The point of tunneling is to serve one of your local port (here `localhost:5000`) on a url (such as `random.yourdomain.com`)

### Why ?

If you want to mimic the behavior of you app when accessed from the outside

## Local Tunneling
Advantage : easy
Draw back : not accessible form the outside

The instructions here are written for a macOS 10.13.3 
### Step One : serve your app `localhost:80`
1. Download nginx
```sh
brew install nginx
```
To stop nginx, run
```sh
nginx -s stop
```

2. Configure nginx
```sh
server {
        listen       80;
        server_name  anna.anna-livia.com;

        location / {
            proxy_pass http://localhost:5000;
            proxy_http_version 1.1;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
```

3. Open your browser to localhost:80

### Step Two : Serve localhost when requesting `random.yourdomain.com`

1. Open /etc/hosts 
```sh
sudo vim etc/hosts
```
2. Add the domain
```sh
127.0.0.1	random.yourdomain.com
```
3. Access `random.yourdomain.com` from your browser
