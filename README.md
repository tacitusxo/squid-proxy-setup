# squid-proxy-setup

Shell scripts to quickly set up a **Squid proxy server with Basic Authentication** on CentOS 7 or Ubuntu 22.

## Features

- Installs and configures Squid proxy server
- Sets up Basic Authentication (username / password)
- Opens the specified port via firewall (`firewalld` / `ufw`)
- Hides proxy headers to improve anonymity
  - `X-Forwarded-For`, `Via`, `Cache-Control` headers are stripped
  - `forwarded_for off` to prevent IP leakage
- Enables Squid as a systemd service (auto-start on reboot)

## Supported OS

| Script | OS |
|---|---|
| `CentOS7-BasicAuthentication.sh` | CentOS 7 |
| `Ubuntu22-BasicAuthentication.sh` | Ubuntu 22 |

## Usage

```bash
sh <script> <username> <password> <port>
```

### CentOS 7

```bash
sh CentOS7-BasicAuthentication.sh myuser mypassword 3128
```

### Ubuntu 22

```bash
sh Ubuntu22-BasicAuthentication.sh myuser mypassword 3128
```

### Arguments

| # | Description | Example |
|---|---|---|
| 1 | Proxy username | `myuser` |
| 2 | Proxy password | `mypassword` |
| 3 | Port number | `3128` |

## Requirements

- Root or sudo privileges
- **CentOS 7**: `yum`, `httpd` (for `htpasswd`), `expect`
- **Ubuntu 22**: `apt`, `openssl`

> The scripts install missing packages automatically.

## What the scripts do

1. Remove any existing Squid installation and config
2. Install Squid (and required tools)
3. Open the specified port on the firewall
4. Create an `.htpasswd` credential file for the given user
5. Inject Basic Auth and anonymization settings into `squid.conf`
6. Enable and start the Squid service

## License

[MIT](https://en.wikipedia.org/wiki/MIT_License)
