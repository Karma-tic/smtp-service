# SMTP Service (Listmonk Infrastructure)

This repository contains the infrastructure as code (Docker Compose) required to run a high-performance, self-hosted email marketing and newsletter platform powered by [Listmonk](https://listmonk.app/).

It includes **Caddy** built-in, which means it will automatically handle your domain routing and fetch a free, auto-renewing HTTPS/SSL certificate for you. **You do not need Coolify or a managed PaaS to host this.**

## Prerequisites
- A VPS (DigitalOcean, Hetzner, AWS, etc.) with Ubuntu or Linux.
- Docker & Docker Compose installed on the server.
- A domain name (e.g., `newsletter.yourdomain.com`) with its DNS A-Record pointed to your VPS IP address.

## Quick Start (Deploying to your server)

1. **Clone this repo to your server:**
   ```bash
   git clone https://github.com/Karma-tic/smtp-service.git
   cd smtp-service
   ```

2. **Set up environment variables:**
   ```bash
   cp .env.example .env
   nano .env  # Set your secure passwords
   ```

3. **Configure your Domain:**
   Open the `Caddyfile` and replace `newsletter.yourdomain.com` with your actual domain name:
   ```bash
   nano Caddyfile
   ```

4. **Initialize the Database:**
   Listmonk requires a one-time setup to create its database tables:
   ```bash
   docker-compose run --rm app sh -c "yes | ./listmonk --install"
   ```

5. **Start the Service:**
   ```bash
   docker-compose up -d
   ```

6. **Access the Dashboard:**
   Navigate to `https://newsletter.yourdomain.com`. Caddy will automatically secure it with HTTPS. Log in with the `ADMIN_USERNAME` and `ADMIN_PASSWORD` you set in your `.env` file.

## Connecting an SMTP Relay
To actually send emails, log in to the Listmonk dashboard, navigate to **Settings > SMTP**, and enter the credentials for your mail provider (e.g., SendGrid, Amazon SES, Mailgun, Postmark).
