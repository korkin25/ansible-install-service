# Ansible Role for Service Management

## Description

This Ansible role is designed for managing various system services. It provides functionality for debugging service configurations, installing service packages, setting facts for current services, deploying configuration files from Jinja2 templates, and triggering service restarts on configuration changes. The role is suitable for deployment on most Debian/Ubuntu-based systems and utilizes standard Ansible modules.

## Features

- Debugging configurations for each service.
- Installation of service packages.
- Setting facts for the current service.
- Deployment of configuration files from Jinja2 templates.
- Triggering service restarts on configuration changes.

## Requirements

- Ansible 2.14 or higher.
- Access to a repository containing the service packages (typically the default OS repositories).

## Role Variables

The role uses the following variables which can be defined in the playbook:

- `services`: A dictionary of services to manage. Each service can have the following attributes:
  - `packages`: A list of packages to be installed for the service.
  - `enabled`: A boolean to indicate if the service should be enabled and managed.
  - `configs`: A dictionary of configuration templates to deploy.

## Example Inventory

Here's an example inventory to demonstrate how to use this role:

```yaml
services:
  nginx:
    packages:
      - "nginx-extras"
    enabled: true
    configs:
      secure-link:
        src: "files/nginx/secure-link.conf.j2"
        dest: "/etc/nginx/sites-enabled/secure-link.conf"
        mode: "0644"
        owner: root
        group: root
        enabled: true
        template_vars:
          template_vars: value
      nginx_conf:
        src: "files/nginx/nginx.conf.j2"
        dest: "/etc/nginx/nginx.conf"
        mode: "0644"
        owner: root
        group: root
        enabled: true
  fail2ban:
    packages:
      - "fail2ban"
    enabled: true
