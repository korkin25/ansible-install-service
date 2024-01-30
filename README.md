# Ansible Role for Service Management

## Description

This Ansible role is designed for managing various system services. It provides functionality for installing, configuring, and managing services such as nginx and fail2ban. The role utilizes standard Ansible modules and is suitable for deployment on most Debian/Ubuntu-based systems.

## Features

- Installation of service packages.
- Deployment of configuration files from Jinja2 templates.
- Automatic service restart on configuration change.
- Error handling with log retrieval for troubleshooting.

## Requirements

- Ansible 2.14 or higher.
- Access to a repository containing the service packages (typically the default OS repositories).

## Role Variables

The role uses the following variables which can be defined in the playbook:

- `services`: A dictionary of services to manage. Each service can have the following attributes:
  - `package`: A list of packages to be installed for the service.
  - `unit_name`: The name of the service unit.
  - `enabled`: A boolean to indicate if the service should be enabled and managed.
  - `log_file`: The path to the service's log file (optional).
  - `configs`: A dictionary of configuration templates to deploy.

## Example Inventory

Here's an example inventory to demonstrate how to use this role:

```yaml
services:
  nginx:
    package:
      - "nginx-extras"
    unit_name: "nginx"
    enabled: true
    log_file: "/var/log/nginx/error.log"
    configs:
      secure-link:
        src: "files/nginx/secure-link.conf.j2"
        dest: "/etc/nginx/sites-enabled/secure-link.conf"
        mode: "0644"
        owner: root
        group: root
        enabled: true
      nginx_conf:
        src: "files/nginx/nginx.conf.j2"
        dest: "/etc/nginx/nginx.conf"
        mode: "0644"
        owner: root
        group: root
        enabled: true
  fail2ban:
    package:
      - "fail2ban"
    unit_name: "fail2ban"
    enabled: true
