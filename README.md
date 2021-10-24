# Ansible Role: pushsafer-webhook-docker

Ansible role to create pushsafer-webhook docker container.

## Mandatory Role Variables

This role requires you to set the address on which pushsafer webhook should listen.

```
pushsafer_webhook_docker__listen_address: "{{ ansible_host }}"
```

The container will be exposed to the _pushsafer_webhook_docker__listen_address_ on port 39196.

This role requires a secret key for flask:

```
pushsafer_webhook_docker__secret_key: !vault |
          $ANSIBLE_VAULT;1.1;AES256
```

The communication between alertmanager and the pushsafer webhook requires http basic auth username and password to be set:

```
pushsafer_webhook_docker__auth_username: "authuser"
pushsafer_webhook_docker__auth_password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
```

Please note that the same credentials need to be set within the alertmanager configuration.

Authentication against the Pushsafer API requires the private key which can be found on the website.
Also the device or group of devices which should receive the push need to be set.

```
pushsafer_webhook_docker__pushsafer_privatekey: !vault |
          $ANSIBLE_VAULT;1.1;AES256
pushsafer_webhook_docker__pushsafer_device_or_group: "dg123"'
```

## Optional Role Variables

Specify the pushsafer webhook version you want to deploy:

```
pushsafer_webhook_docker__pushsafer_webhook_version: "v2.30.3"
```
