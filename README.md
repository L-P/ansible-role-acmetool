ansible-role-acmetool
=====================
Install, configure and run `acmetool` to generate Let's Encrypt TLS certificates.

`acmetool` will be configured to use its `redirector` mode. It will listen on
port 80 and redirect ([HTTP 308](https://tools.ietf.org/html/rfc7238)) anything
that is not a challenge request.

See [acme](https://github.com/hlandau/acme) on GitHub for details.

Requirements
------------
* This was only tested on an ARM version of Ubuntu 16.04.  Acmetool needs to be
  run as a regular user on ARM because it can't drop privileges, this role was
  specifically made to run acmetool as its own user.

* `become: true` is required as most actions need to be run as root, the rest
  is run under `acme` which will be created by the role.

* `ufw` is expected to be present, it was not installed by default on my system.

* As the `redirector` mode is used, no HTTP server is required to run. You can
  install whatever server you want to run **after** running this role so it can
  use the generated certificates.

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
# URL of the LetsEncrypt agreement to accept
acmetool_agreement_url: "https://example.com/TOS.pdf"
```

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
