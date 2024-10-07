# Watch nginx logs

To watch NGINX logs in real-time, you can use the `tail` command, which allows you to follow the log file as new entries are added. NGINX typically stores logs in two main log files:

- **Access logs**: Information about client requests to the server.
- **Error logs**: Information about server errors or issues.

# Common NGINX Log File Locations

- **Access log**: `/var/log/nginx/access.log`
- **Error log**: `/var/log/nginx/error.log`

These are the default locations, but they can vary depending on how NGINX is configured (check `/etc/nginx/nginx.conf` file).

If your logs are stored in non-standard locations, you can find the log paths in your NGINX configuration file (`/etc/nginx/nginx.conf` or files in `/etc/nginx/conf.d/`):
```bash
grep "access_log" /etc/nginx/nginx.conf
grep "error_log" /etc/nginx/nginx.conf
```

# Summary

- **Watch access log**: `tail -n 10 -f /var/log/nginx/access.log`
- **Watch error log**: `tail -n 10 -f /var/log/nginx/error.log`
- **Watch both logs**: `tail -n 10 -f /var/log/nginx/access.log /var/log/nginx/error.log`
- **Filter logs**: `tail -n 10 -f /var/log/nginx/access.log | grep "keyword"`

**Using `multitail` for Better Visualization**

For a more advanced, multi-file tailing tool, you can install `multitail`, which allows you to view multiple log files with color highlighting and better organization.

To install `multitail`:
```bash
sudo apt-get install multitail  # Debian/Ubuntu
sudo yum install multitail      # CentOS/RHEL
```

After installation, use it to watch multiple NGINX logs:
```bash
multitail /var/log/nginx/access.log /var/log/nginx/error.log
```
