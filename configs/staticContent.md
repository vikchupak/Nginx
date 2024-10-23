https://docs.nginx.com/nginx/admin-guide/web-server/serving-static-content/

- The `root` directive specifies the root directory that will be used to search for a file.

# Default location for static content

The `/usr/share/nginx/html` directory is the default location where Nginx serves web content on many Linux-based systems. This is the folder that Nginx is pre-configured to serve files from when you install it, unless the configuration is changed.

Here’s more detail about this directory:

### Purpose of `/usr/share/nginx/html`:
- **Default Web Root**: After installing Nginx, the `/usr/share/nginx/html` directory acts as the default root for serving static HTML files, images, CSS, JavaScript, and other web content.
- **Default Landing Pages**: By default, this directory contains a file like `index.html`, which is the landing page shown when you access your server's IP address or domain name without any additional path (e.g., `http://your-server-ip/`).
  
### Example Structure:
After a fresh Nginx installation, you may find files like:

```bash
/usr/share/nginx/html/
    ├── 404.html
    ├── index.html
```

- **`index.html`**: This is typically the default page that gets loaded when you visit your server's root URL.
- **`404.html`**: This is a default error page that may be served when Nginx encounters a "404 Not Found" error.

### How Nginx Uses It:
In the default Nginx configuration file (usually located at `/etc/nginx/nginx.conf` or `/etc/nginx/sites-available/default`), the following line defines this folder as the root directory for serving files:

```nginx
server {
    listen 80;
    server_name localhost;

    root /usr/share/nginx/html;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

This means that when someone visits your server (e.g., `http://your-server-ip/`), Nginx will look in `/usr/share/nginx/html` for the `index.html` file to serve to the browser.

Real config file example\
https://github.com/VIK2395/nest-app_dockerized/blob/master/volumes/nginx/etc-nginx/conf.d/default.conf.backup#L9
