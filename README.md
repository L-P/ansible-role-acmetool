# ansible-role-acmetool
Install, configure and run `acmetool` to generate Let's Encrypt TLS certificates.

See [acme](https://github.com/hlandau/acme) on GitHub for details.

## Requirements
This was only tested on an ARM version of Ubuntu 16.04.  
Acmetool needs to be run as a regular user on ARM because it can't drop
privileges, this role was specifically made to run acmetool as its own user.

`ufw` is expected to be present, it was not installed by default on my system.

## Required vars
```yaml
# Address used to register domains with LetsEncrypt.
acmetool_email: "contact@example.com"
# space-separated list of domains to register.
acmetool_domains: "www.example.com example.com"
```

## Other vars
```yaml
# URL of the LetsEncrypt agreement to accept
acmetool_agreement_url: "https://example.com/TOS.pdf"
```
