# Load Balancer

## Project Overview
This project configures a redundant web infrastructure using two Nginx web servers (web-01, web-02) behind an HAProxy load balancer (lb-01).

## Files

### `0-custom_http_response_header`
Configures a brand new Ubuntu server with Nginx and adds a custom HTTP response header:
- **Header name:** `X-Served-By`
- **Header value:** The hostname of the server (e.g., `6983-web-01` or `6983-web-02`)

**Usage:**
```bash
sudo bash 0-custom_http_response_header
```

**Verify:**
```bash
curl -sI <server-ip> | grep X-Served-By
```

### `1-install_load_balancer`
Installs and configures HAProxy on lb-01 to:
- Listen on port 80
- Distribute traffic using **round-robin** between web-01 and web-02

**Usage:**
```bash
sudo bash 1-install_load_balancer
```

**Verify:**
```bash
# Run multiple times — X-Served-By should alternate between web-01 and web-02
curl -sI <lb-01-ip> | grep X-Served-By
```

## Servers
| Name        | Role          |
|-------------|---------------|
| 6983-web-01 | Web server 1  |
| 6983-web-02 | Web server 2  |
| 6983-lb-01  | Load balancer |

## Requirements
- Ubuntu 16.04 LTS
- Nginx (web servers)
- HAProxy (load balancer)
