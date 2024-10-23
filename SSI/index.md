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
So, the directive MUST return HTML or text data that can be inserted directly into the HTML file being processed.
