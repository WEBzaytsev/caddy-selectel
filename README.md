# Selectel DNS v2 module for Caddy

This package contains a DNS provider module for [Caddy](https://github.com/caddyserver/caddy). It can be used to manage DNS records with [Selectel DNS v2 API](https://developers.selectel.ru/docs/cloud-services/dns_api/dns_api_actual/).

## Caddy module name

```
dns.providers.selectel
```

## Config examples

To use this module for the ACME DNS challenge, [configure the ACME issuer in your Caddy JSON](https://caddyserver.com/docs/json/apps/tls/automation/policies/issuer/acme/) like so:

```json
{
  "module": "acme",
  "challenges": {
    "dns": {
      "provider": {
        "name": "selectel",
        "user": "SELECTEL_USER", // see link "Selectel Service user" below
        "password": "SELECTEL_PASSWORD",
        "account_id": "SELECTEL_ACCOUNT_ID", // your main Selectel account id, like "123456"
        "project_name": "SELECTEL_PROJECT_NAME" // a project in which the service user is an administrator
      }
    }
  }
}
```

or with the Caddyfile:

```
# globally
{
	acme_dns selectel {
		user {env.SELECTEL_USER}
		password {env.SELECTEL_PASSWORD}
		account_id {env.SELECTEL_ACCOUNT_ID}
		project_name {env.SELECTEL_PROJECT_NAME}
	}
}
```

```
# one site
tls {
	dns selectel {
		user {env.SELECTEL_USER}
		password {env.SELECTEL_PASSWORD}
		account_id {env.SELECTEL_ACCOUNT_ID}
		project_name {env.SELECTEL_PROJECT_NAME}
	}
}
```

**Note:** Debug logging is enabled by default. All DNS operations from `selectel-libdns` will appear in Caddy logs.

Selectel [Service user](https://my.selectel.ru/iam/users_management/users?type=service) management


## Fork & Credits

This repository is a fork of:

- [jjazzme/selectelv2-caddy](https://github.com/jjazzme/selectelv2-caddy)
- [caddy-dns/selectel](https://github.com/caddy-dns/selectel)

Special thanks to [@jjazzme](https://github.com/jjazzme) for the original work and idea.
