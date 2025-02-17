https://nginx.org/en/docs/http/ngx_http_ssi_module.html

Nginx Server Side Includes (SSI) is a feature that allows dynamic content to be inserted into HTML files on the server side before sending it to the client. It’s useful for reusing parts of a webpage (like headers, footers, or other common elements) across multiple pages, without having to duplicate the content manually.

### How to Enable SSI in Nginx
To use SSI in Nginx, you need to enable the `ssi` and `ssi on` directives in your configuration file. Here’s an example configuration snippet:

```nginx
server {
    listen 80;
    server_name example.com;
    
    location / {
        root /var/www/html;
        ssi on;  # Enables SSI processing
        ssi_types text/html;  # Specifies MIME types that should be processed (usually HTML)
    }
}
```

### Example SSI Directive

```html
<!--# include virtual="/remote/body.php?argument=value" -->
```

- **`#include`**: This directive is used to include files or the output of another resource into the current HTML.
- **`virtual="/remote/body.php?argument=value"`**: This tells Nginx to include the output of `/remote/body.php?argument=value`. The `virtual` attribute is used to indicate a URL or path that Nginx can serve, either locally or remotely.

This SSI directive includes the output of an external resource into the current file.
Nginx SSI is typically used for HTML documents, and it expects the included content to be something that can be rendered within an HTML page.
So, **the directive MUST return HTML or text data** that can be inserted directly into the HTML file being processed.

# Virtual path and hostname

When using **`virtual="..."`** in an Nginx **SSI (`#include`) directive**, the request is handled internally by Nginx. This means:  

- The hostname in `virtual="..."` refers to **the same Nginx server handling the current request**.  
- Nginx processes the URI as if it were requested directly by a client.  
- It does **not** automatically proxy to external servers unless additional configurations (like `proxy_pass`) are set up.  

### Example: Internal Request  
#### **Nginx Configuration**
```nginx
server {
    listen 80;
    server_name example.com;

    ssi on;

    location / {
        root /var/www/html;
    }

    location /remote/ {
        root /var/www/html;
        index body.php;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
#### **HTML File (`index.html`)**
```html
<!--# include virtual="/remote/body.php?argument=value" -->
```
- The SSI request to `/remote/body.php?argument=value` is handled **internally** by Nginx.
- It is equivalent to opening `http://example.com/remote/body.php?argument=value`.

---

### What If You Need an External Server?  
If you want to include content from another server (e.g., `http://external.com/data`), SSI alone **cannot** do this directly. Instead, you must use **proxying**:

#### **Solution: Proxy to External Server**
```nginx
location /external/ {
    proxy_pass http://external.com/;
}
```
Then in your HTML:
```html
<!--# include virtual="/external/data" -->
```
Now, the request fetches content from `http://external.com/data`.
