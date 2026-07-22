# Laravel stack for Wodby

Deploy Laravel on Kubernetes with Wodby. This repository contains the stack
manifests used by the public Laravel stack in the Wodby catalog.

- [Laravel stack in the Wodby catalog](https://wodby.com/stacks/laravel)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## What's included

| Component / service | Default configuration |
| --- | --- |
| PHP<br>`laravel-php` | required; enabled by default; versions: `8.5` by default; also available: `8.3`, `8.4`; volumes: `storage` 20 GB; links: `db` → `mariadb`, `redis` → `valkey`, `storage` → `files-nfs`, `sendmail` → `mailpit`; derivatives: `sshd` → `laravel-php-sshd`, `queue` → `laravel-php-queue` |
| Nginx<br>`laravel-nginx` | required; enabled by default; links: `backend` → `php` |
| MariaDB<br>`mariadb` | required; enabled by default; volumes: `data` 10 GB |
| Files NFS storage (`files-nfs`)<br>`nfs-provisioner` | optional; enabled by default; volumes: `data` 25 GB |
| Valkey<br>`valkey` | required; enabled by default |
| Mailpit<br>`mailpit` | optional; enabled by default |
| OpenSMTPD<br>`opensmtpd` | optional; disabled by default |
| Gotenberg<br>`gotenberg` | optional; disabled by default |
| Cloud MariaDB (`cloud-mariadb`)<br>`cloud-mariadb` | optional; disabled by default; versions: `10.3` by default |
| Cloud MySQL (`cloud-mysql`)<br>`cloud-mysql` | optional; disabled by default; versions: `5.7` by default; also available: `8` |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Use this stack

The simplest path is to add the public stack from the Wodby catalog. Review the
enabled services, versions, storage sizes, links, and other defaults when
creating your app.

To maintain your own version of this stack:

1. Fork this repository.
2. Edit the stack manifest.
3. Import the repository as a
   [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

Wodby imports the manifest from the selected Git branch or tag and creates a new
stack revision when the Git-backed stack is updated.

## Customize the stack

Common changes include selecting different service versions, enabling or
disabling optional components, changing persistent volume sizes, adjusting
stack-level environment and workload overrides, or replacing one linked service
with another compatible service.

When replacing or renaming a stack service, update every corresponding
`services[].links` target and derivative reference. Stack-local names and
referenced service names are distinct identifiers and do not need to match.

Validate customized manifests with the Wodby CLI before importing them:

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

See the [stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)
for every supported field and the [managed services
index](https://github.com/wodby/services) for available service references.
