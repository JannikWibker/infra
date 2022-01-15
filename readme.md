# Infra

This repository aims to include all infrastructure related things that are needed to run my home server setup.

The main components used are:
- ansible
- docker with docker-compose


## What is included?

The following services will be run:
- personal identity provider (auth) (WIP)
- local dns server (bind9)
- bitwarden (vaultwarden)
- git server (gitea)
- nextcloud (WIP)
- plex
- portainer
- network shares (samba) (WIP)
- school-docs
- traefik
- personal website
- web-based photo gallery (photoprism)

## Getting started

To run this the following has to be done / configured:

- Install ubuntu server on your target system
- Create a user called `docker-user`
- Add `docker-user` to the sudo group (or wheel group)
- Set a password for the user
- Generate an ssh key for the target system (`ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/<HOSTNAME_OF_TARGET_MOST_LIKELY> -C <YOUR_EMAIL_ADDRESS_FOR_EASY_IDENTIFICATION>`)
- Copy an ssh key to /home/docker-user/.ssh ([like described here](https://developers.redhat.com/blog/2018/11/02/how-to-manually-copy-ssh-keys-rhel))
- Ensure the ssh key works and update the `hosts` file with the correct file location
- Ensure the other variables in the `hosts` file are also correct
- Generate an ansible-vault:
  - `cd group_vars/all`
  - `rm secret.yml`
  - `ansible-vault create secret.yml` and add a passphrase
  - copy the structure described below and fill in the missing variables
- Modify `group_vars/all/vars.yml` as much as you like
- Run `ansible-playbook playbook.yml -K --ask-vault-pass`


## ansible-vault

> Currently no secrets are needed, this may change in the future.

This is the structure of my secret.yml file:

```yaml
photoprism:
  ADMIN_PASSWORD: "..." # this only sets the initial password, updating later on can be done using the web interface
  DB_PASSWORD: "..."

gitea: # gitea generates these values itself when they can't be found in the config file; start gitea without them and extract them afterwards
  LFS_JWT_SECRET: "..."
  INTERNAL_TOKEN: "..."
  SECRET_KEY: "..."
```


## Comments about services

TODO: add some kind of description about services and how they are deployed
