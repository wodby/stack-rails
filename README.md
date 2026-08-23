# Rails application stack for Kubernetes on Wodby

Deploy Rails applications on Kubernetes with Wodby.

This repository defines the Wodby stack manifests and default service
composition for Rails.

<!-- wodby:generated:start -->

## Stack contract

- [Rails stack on Wodby](https://wodby.com/stacks/rails)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Start from a boilerplate

Use one of the compatible boilerplates exposed by this stack's services to
start with Wodby CI build configuration:

- [Rails boilerplate](https://github.com/wodby/rails-boilerplate)

## Service definitions

- [Ruby (Rails) service](https://github.com/wodby/service-rails)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [Valkey service](https://github.com/wodby/service-valkey)
- [Mailpit service](https://github.com/wodby/service-mailpit)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)
- [Gotenberg service](https://github.com/wodby/service-gotenberg)
- [Cloud PostgreSQL service](https://github.com/wodby/service-cloud-postgres)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Ruby<br>`rails` | required; enabled by default; links: `db` → `postgres`, `redis` → `valkey`, `sendmail` → `mailpit` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 20 GB |
| Valkey<br>`valkey` | required; enabled by default; volumes: `data` 5 GB |
| Mailpit<br>`mailpit` | optional; disabled by default |
| OpenSMTPD<br>`opensmtpd` | optional; disabled by default |
| Gotenberg<br>`gotenberg` | optional; disabled by default |
| Cloud PostgreSQL<br>`cloud-postgres` | optional; disabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Background jobs

The Rails boilerplate uses Sidekiq by default. Its worker derivative is enabled
and the required Rails-to-Valkey link supplies `REDIS_URL`. Valkey uses
persistent storage and a `noeviction` memory policy suitable for queue data.

## Deploy this stack

Start from [Rails boilerplate](https://github.com/wodby/rails-boilerplate), or connect your own compatible source
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
