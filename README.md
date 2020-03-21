Cloudflare
=========

Cloudflare DNS records managment role

Requirements
------------

Requires Cloudflare account and admin API key.

Role Variables
--------------

 Variable | Description | Default value | Required
------------ | ------------- | ------------- | -------------
cloudflare_account_email | Account email. | none | Yes
cloudflare_account_api_token | Account API token. You can obtain your API key from the bottom of the Cloudflare 'My Account' page, found here: https://dash.cloudflare.com/ | none | Yes
cloudflare_dns_records.zone | DNS zone to mange. | none | Yes
cloudflare_dns_records.records | DNS record to mange (described below). | none | Yes


```cloudflare_dns_records.records``` (https://docs.ansible.com/ansible/latest/modules/cloudflare_dns_module.html#id3)


 Key | Description | Default value | Required
------------ | ------------- | ------------- | -------------
name | DNS name | @ | No
type | The type of DNS record to create. | none | If `state: present`
value | The record value as quoted string or unqoted IP. | none | If `state: present`
priority | Record priority. | 1 | Required for `type: MX` and `type: SRV`
ttl | The TTL to give the new record. Must be between 120 and 2,147,483,647 seconds, or 1 for automatic. | 1 | No
state | Whether the record(s) should exist or not. | present | no
solo | Whether the record should be the only one for that record type and record name. Only use with `state: present`. This will delete all other records with the same record name and type. | Yes | No
proxied | Proxy through Cloudflare network or just use DNS. | no | no


Example config
--------------

```
cloudflare_account_email: foo@bar.com
cloudflare_account_api_token: xxx
```

DNS records:

```
cloudflare_dns_records:
  - zone: foobar.com
    records:
      - type: MX
        priotity: 1
        ttl: 3600
        value: 'aspmx.l.google.com.'
        solo: false
      - type: MX
        priotity: 5
        ttl: 3600
        value: 'alt1.aspmx.l.google.com.'
        solo: false
      - type: MX
        priotity: 5
        ttl: 3600
        value: 'alt2.aspmx.l.google.com.'
        solo: false
      - type: MX
        priotity: 10
        ttl: 3600
        value: 'alt3.aspmx.l.google.com.'
        solo: false
      - type: MX
        priotity: 10
        ttl: 3600
        value: 'alt4.aspmx.l.google.com.'
        solo: false
      - name: cname-record
        type: CNAME
        value: hgs.google.com
      - name: a-record
        type: A
        value: 45.68.13.8
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - cloudflare

License
-------

BSD

Author Information
------------------

If You like this role and would like to buy me :coffee: or :beer: You can do it via [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=2NJYFLHNYJGU2&item_name=Ansible+Role+Development&currency_code=PLN&source=url)
