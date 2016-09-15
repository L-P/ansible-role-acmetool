ansible-role-acmetool
=====================
Install, configure and run `acmetool` to generate Let's Encrypt TLS certificates.

`acmetool` will be configured to use its `redirector` mode. It will listen on
port 80 and redirect ([HTTP 308](https://tools.ietf.org/html/rfc7238)) anything
that is not a challenge request.

See [acme](https://github.com/hlandau/acme) on GitHub for details.

Requirements
------------
* `become: true` is required as most actions need to be run as root, the rest
  is run under `acme` which will be created by the role.

* You need to open port 80/TCP for `acmetool` to serve challenges.

* As the `redirector` mode is used by default, no HTTP server is required to
  run. You can install whatever server you want to run **after** running this
  role so it can use the generated certificates.

* Chose your provider and set its API endpoint in `acmetool_server`, see below.

* The `cron` package is required for automatic renewal.

Role Variables
--------------
## Required
```yaml
# Address used to register domains with LetsEncrypt.
acmetool_email: "contact@example.com"
# space-separated list of domains to register.
acmetool_domains: "www.example.com example.com"
```

## Other
```yaml
# CA server. This defaults to the acme-staging server for testing purposes.
# You will need to change this to the production server :
# https://acme-v01.api.letsencrypt.org/directory
acmetool_server: "https://acme.example.com/directory"

# Change this to RSA if your server does not support EC keys (eg. murmur).
acmetool_key_type: "ecdsa"

# If you don't trust acmetool to run hooks as root (sudo), set this to false.
acmetool_enable_hooks: false
```

See [the defaults](defaults/main.yml) for the complete list.

Example Playbook
----------------
```yaml
- hosts: all
  roles:
    - { role: "L-P.acmetool", become: true }
```

License
-------
MIT
