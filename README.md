# Ansible Roles: LetsEncrypt_DigitalOcean

This role can be used to generate certificates provided by LetsEncrypt using the DNS challenge method.  This role assumes that you have a domain, and you have it configured to use DigitalOcean nameservers.

## Requirements

On the host you are running this from you will need the python cryptography libraries.
Example for Ubuntu:  ```apt install python3-cryptography```

## Role Variables

A few variables need to be set in order to use this role.

### Required Variables

Set an email address to use with LetsEncrypt

```yaml
le_do_mailaddr: noe@example.com
```

Set the domain for which you would like to get a certificate (the generated one will be valid for a wildcard cert, ie "*.engonzal.com" and the base domain "engonzal.com")

```yaml
le_do_domain: example.com
```

You will need to generate an oauth token via the DigitalOcean admin console

```yaml
le_do_token: "<your-do-token-consider-using-ansible-vault>"
```

### Optional Variables

You can customize where the certificates are stored by setting the following (default is a data directory in your user home folder):

```yaml
le_do_dir_priv: "~/data/acme"
le_do_dir_cert: "~/data/certs"
```

You can also optionally upload your newely created certificate to DigitalOcean:

```yaml
le_do_upload: true
```

## Example Playbook

```yaml
- hosts: proxmox
  user: engonzal
  vars:
    le_do_mailaddr: noe@example.com
    le_do_domain: example.com
    le_do_token: "<your-do-token-consider-using-ansible-vault>"
  roles:
      - engonzal.letsencrypt_do
```

## License

BSD

## Author Information

This role was created on a saturday morning with a cup of coffee in 2019 by Noe Gonzalez (<http://engonzal.com> and <https://buildahomelab.com>)
