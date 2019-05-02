# Default Nginx Configuration

Reference for new servers needing Nginx configuration. Includes:

- Modern, secure SSL.
- FastCGI cache.

## Prerequisites

Install `envsubst` command from the `gettext` package.
On macOS you need to run the following commands to be able to use it correctly:

```bash
brew install gettext
brew link --force gettext
```

## Compiling The Template

There is a template for site configuration located at `template/site.conf`.
To create the configuration for the domain `<DOMAIN>` run the following command:

```bash
DOMAIN="<DOMAIN>" envsubst < "template/site.conf" > "sites-available/<DOMAIN>.conf"
```

## Installing Certificates

Install [Certbot](https://certbot.eff.org/).

```
sudo mkdir -p "/etc/letsencrypt/challenges"
sudo certbot certonly --webroot -w "/etc/letsencrypt/challenges" --cert-name="<DOMAIN>" -d "<DOMAIN>" -d "www.<DOMAIN>"
```

Enable automatic certificate renewals in the CRON by adding the following line
into the editor when running the command `sudo crontab -e`.

```
0 3 * * * certbot renew --quiet
```
