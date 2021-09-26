Role Name
=========

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) 

Ansible playbook install and configure nginx.


Requirements
------------

 - Ubuntu

Playbook Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------
```YAML
---
- hosts: all
  tasks:
    - name: Ensure nginx is at the latest version
      apt: name=nginx state=latest
      become: yes
    - name: Start nginx
      service:
          name: nginx
          state: started
      become: yes
    - name: Copy the main nginx config file and restart nginx
      copy:
        src: /template/nginx.conf
        dest: /etc/nginx/nginx.conf
      become: yes
    - name: Copy config for status.conf
      file:
        src: /template/status.conf.j2
        dest: /etc/nginx/conf.d/status.conf
      become: yes
    - name: Copy config for wordpress
      copy:
        src: /template/wordpres.j2
        dest: /etc/nginx/sites-enabled/wordpress
      become: yes
    - name: Copy config for bookstack
      copy:
        src: /template/bookstack.j2
        dest: /etc/nginx/sites-enabled/bookstack
      become: yes
    - name: Restart nginx
      service:
        name: nginx
        state: restarted
      become: yes
```
