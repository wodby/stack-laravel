# Laravel application stack for Kubernetes on Wodby

Deploy Laravel applications on Kubernetes with Wodby.

This repository defines the Wodby stack manifests and default service
composition for Laravel.

<!-- wodby:generated:start -->

## Stack contract

- [Laravel stack on Wodby](https://wodby.com/stacks/laravel)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Start from a boilerplate

Use one of the compatible boilerplates exposed by this stack's services to
start with Wodby CI build configuration:

- [Laravel on Wodby](https://github.com/wodby/laravel-boilerplate)

## Service definitions

- [PHP (Laravel) service](https://github.com/wodby/service-laravel-php)
- [Nginx (Laravel) service](https://github.com/wodby/service-laravel-nginx)
- [MariaDB service](https://github.com/wodby/service-mariadb)
- [Ganesha NFS provisioner service](https://github.com/wodby/service-nfs-provisioner)
- [Valkey service](https://github.com/wodby/service-valkey)
- [Mailpit service](https://github.com/wodby/service-mailpit)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)
- [Gotenberg service](https://github.com/wodby/service-gotenberg)
- [Cloud MariaDB service](https://github.com/wodby/service-cloud-mariadb)
- [Cloud MySQL service](https://github.com/wodby/service-cloud-mysql)

## What's included

| Component / service | Default configuration |
| --- | --- |
| PHP<br>`php` | required; enabled by default; volumes: `storage` 20 GB; links: `db` → `mariadb`, `redis` → `valkey`, `storage` → `files-nfs`, `sendmail` → `mailpit` |
| Nginx<br>`nginx` | required; enabled by default; links: `backend` → `php` |
| MariaDB<br>`mariadb` | required; enabled by default; volumes: `data` 10 GB |
| Files NFS storage<br>`files-nfs` | optional; enabled by default; volumes: `data` 25 GB |
| Valkey<br>`valkey` | required; enabled by default |
| Mailpit<br>`mailpit` | optional; enabled by default |
| OpenSMTPD<br>`opensmtpd` | optional; disabled by default |
| Gotenberg<br>`gotenberg` | optional; disabled by default |
| Cloud MariaDB<br>`cloud-mariadb` | optional; disabled by default |
| Cloud MySQL<br>`cloud-mysql` | optional; disabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Deploy this stack

Start from [Laravel on Wodby](https://github.com/wodby/laravel-boilerplate),
which includes `.wodby/pipeline.yml`, or connect your own compatible source
repository.

Review service versions, storage, links, and optional components when creating
the application. The same stack can be reused across development, staging, and
production environments.

## Maintain a custom version

1. Fork this repository.
2. Edit the stack manifest.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target
and derivative reference. Stack-local names and referenced service names are
distinct identifiers.
