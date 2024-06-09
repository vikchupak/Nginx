# Nginx

Terms:
- directives
- server block
- location block
- location can be defined using __prefix (string) or regular expression__
- location block can be placed inside server block or __inside another location block__

About server and location blocks:\
https://www.digitalocean.com/community/tutorials/understanding-nginx-server-and-location-block-selection-algorithms \
https://www.digitalocean.com/community/tutorials/nginx-location-directive
![Screenshot from 2024-06-09 18-14-29](https://github.com/VIK2395/Nginx/assets/50545334/5f5e76d2-b4b8-4359-857b-892dc1b57cc8)
![Screenshot from 2024-06-09 18-13-20](https://github.com/VIK2395/Nginx/assets/50545334/78fc8739-1002-4ec9-89c7-70bca10c04c0)


Directive Inheritance in Nested Location Blocks:\
https://stackoverflow.com/questions/32104731/directive-inheritance-in-nested-location-blocks
![Screenshot from 2024-06-09 18-10-38](https://github.com/VIK2395/Nginx/assets/50545334/cc5ea2d5-d1b0-4d62-81d8-8707f7912c89)


proxy_pass directive => to redirect requests\
https://dev.to/danielkun/nginx-everything-about-proxypass-2ona

```javascript
// variable declaration
set $varName varValue;

// variable usage
proxy_set_header $varName;
```

access_log\
error_log\
root\
server_name
