ansible-railgun
===============

Railgun is a WAN optimization technology developed by CloudFlare and is available to CloudFlare Business and Enterprise customers, as well as Optimized Partners. Railgun requires a piece of software called the Railgun Listener to be installed on your web server's network. This ansible module will install, configureand start the listener service. Any configuration changes will automatically restart railgun.

Requirements
------------

- Redhat or Debian based distribution.
- Outbound tcp/443 to https://pkg.cloudflare.com.
- Outbound tcp/443 to ipify.com.
- Inbound tcp/2408 from Cloudflare.
- Enterprise / business Cloudflare account.

Railgun supported distros
-------------------------

RHEL and CentOS:-

- 7.x
- 6.x

Ubuntu:-

- Xenial (16.04)
- Wily (15.10)
- Vivid (15.04)
- Utopic (14.10)
- Trusty (14.04)
- Precise (12.04)

Debian:-

- Jessie (8)
- Wheezy (7)
- Squeeze (6)

Role Variables
--------------
All Railgun configuration settings are templated, the defaults are kept to those set by the Cloudflare packaging team.

Key settings:-

    railgun_activation_token: obtain this from the Cloudflare web interface
    railgun_activation_railgun_host: external_ip of host (detected from ipify.com)
    railgun_wan_port: (2408)

If you have a local link IPv6 address Railgun will prefer that to an IPv4 address. To force the use of ipv4 you must set this:-

    railgun_wan_ip: "{{ ansible_default_ipv4.address }}"

Fix a listener version with:-

    railgun_packages:
      railgun-stable:
        version: '5.3.0'

Dependencies
------------

Railgun requires memcached (https://memcached.org/) to be installed and (by default) listening on 127.0.0.1:11211 (the default memcached host:port).
You should also increase the CACHESIZE set in memcached.conf from its default 64MB (very low) to at least 2048 (2GB). Further tuning should be done by consulting the memcached documentation around the STAT command.


Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: railgun, railgun_activation_token: <1234567_protect_me_with_vault> }

Testing
-------

Set this yaml:-

    railgun_log_level: 5

https://www.cloudflare.com/docs/railgun/installation.html#testing-railgun


License
-------

GPL3

Author Information
------------------

https://github.com/gilesw


