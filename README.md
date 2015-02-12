# nginx role

Get with ```git clone https://github.com/gitinsky/ansible-role-nginx.git roles/nginx```

Installs nginx, adds two handlers for reload, ```nginx reload``` and ```reload nginx```.

For rpm-based system ```nginx.conf``` will be taken from templates.

# Variables

```nginx_no_default``` is set to ```true``` by default, so it'll remove the default nginx configuration. Set to ```false``` to preserve it.

```root``` is set by default to ```/usr/share/nginx/html``` (redhat only)

# Example

```
---
- hosts: nginx
  sudo: yes
  roles:
  - role: nginx
```

###### Putting your configuratins

```
- name: nginx mysite config
  template: src=nginx/mysite.conf dest=/etc/nginx/sites-available/mysite.conf
  notify: reload nginx
  tags:
      - config

- name: enable nginx mysite config
  file: state=link src=../sites-available/mysite.conf dest=/etc/nginx/sites-enabled/mysite.conf
  notify: reload nginx
  tags:
      - config

```

# Notes
Tested on ubuntu 14.04 and CentOS 6.5, ansible 1.8.2
Failes on centos if you don't have a ```/run``` directory.