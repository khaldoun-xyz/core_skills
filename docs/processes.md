# Khaldoun's process library

- onboarding
  - [first week](#first-week)
- [product maintenance](#product-maintenance)
  - [autodeploy product releases](#autodeploy-product-releases)
  - [autodeploy feature commits](#autodeploy-feature-commits)
  - [(re-)certify ssl](#re-certify-ssl)
- product development
  - [align and execute](#align-and-execute)

## Onboarding

### first week

- Prepare a "Your first day"" message in advance and post it on Basecamp.
- On the first day, ask the candidate to read through the [welcome memo](../README.md)
  and to [set up his/her laptop](../setup/README.md).
- Ask the new member to sign up to
  - [The Batch](https://www.deeplearning.ai/the-batch/) and
  - [Script](https://sisu.cx/script/).

## Product maintenance

### autodeploy product releases

- For initial installation:
  - In your Digital Ocean droplet `/root`,
    run `git clone <repo_url>`,
    create an `.env_[PRODUCT]` file in `/root`
    (necessary for Github Action).
  - In your repo, set up Github Actions by following [this guide](https://medium.com/swlh/how-to-deploy-your-application-to-digital-ocean-using-github-actions-and-save-up-on-ci-cd-costs-74b7315facc2).
    - Use [this Github Actions deploy.yml](https://github.com/khaldoun-xyz/lugha/blob/main/.github/workflows/deploy.yml)
      as a template.

~~~mermaid
---
title: continuously deploy after master/main merge
---
flowchart LR
  A[merge in product's master/main branch] --> B[trigger Github Action]
  B --> C[deploy to Digital Ocean droplet]
  C --> D[end]
~~~

### autodeploy feature commits

- For initial installation:
  - In your Digital Ocean droplet `/root`,
    run `git clone <repo_url>`,
    create an `.env_[PRODUCT]` file in `/root`
    (necessary for Github Action).
  - In your repo, set up Github Actions by following [this guide](https://medium.com/swlh/how-to-deploy-your-application-to-digital-ocean-using-github-actions-and-save-up-on-ci-cd-costs-74b7315facc2).
    - Use [this Github Actions feature.yml](https://github.com/khaldoun-xyz/lugha/blob/main/.github/workflows/feature.yml)
      as a template.

~~~mermaid
---
title: deploy any commit to a feature branch
---
flowchart LR
  A[any commit to a feature branch] --> B[trigger Github Action]
  B --> C[deploy to Digital Ocean droplet]
  C --> D[end]
~~~

### (re-)certify ssl

~~~mermaid
---
title: set up ssl
---
flowchart LR
  A[set up project's docker-compose with gunicorn & nginx service]
  A --> B[in nginx.conf, comment out ssl mentions]
  B --> C[deploy project in droplet]
  C --> D[in droplet's project root, run ssl cert command]
  D --> E[in nginx.conf, activate ssl mentions & redeploy]
  E --> F[end]
~~~

~~~mermaid
--- 
title: recertify ssl
---
flowchart LR
  A[in droplet's project root run ssl cert command]
  A --> B[end]
~~~

- Examples
  - [Lugha's docker-compose.yml](https://github.com/khaldoun-xyz/lugha/blob/main/docker-compose.yml)
  - [Lugha's nginx.conf](https://github.com/khaldoun-xyz/lugha/blob/main/nginx.conf)
  - ssl recert command: ```docker run -it --rm -v $(pwd)/html:/var/www/html
    -v /etc/letsencrypt:/etc/letsencrypt
    certbot/certbot certonly --webroot -w /var/www/html -d lugha.xyz```

- Troubleshooting
  - at initial run
    - `sudo mkdir -p /var/www/html`
    - `sudo chown -R www-data:www-data /var/www/html`
  - firewall problems
    - `sudo ufw allow 80`
    - `sudo ufw allow 443`
    - `sudo ufw allow https`
    - `chmod -R 755 /etc/letsencrypt`
    - `chmod 644 /etc/letsencrypt/live/PROJECT_FOLDER/*.pem`

## Product development

### Align and execute

We do [asynchronous weekly check-ins](/README.md#weekly-check-ins).

~~~mermaid
---
title: Weekly check-ins
---
flowchart LR
  A[start of week notification] --> B[member reflects on progress, sets new plan]
  B --> C[others may comment]
  C --> D[end]
~~~

