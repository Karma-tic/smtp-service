# SMTP Service (Listmonk Infrastructure)

This repository contains the infrastructure as code (Docker Compose) required to run a high-performance, self-hosted email marketing and newsletter platform powered by [Listmonk](https://listmonk.app/).

## Prerequisites
- Docker & Docker Compose installed on your server (or deployment via Coolify).

## Quick Start

1. **Set up environment variables:**
   ```bash
   cp .env.example .env
   ```
   Edit `.env` to set secure passwords.

2. **Initialize the Database:**
   Listmonk requires a one-time setup to create its database tables. Run the following command:
   ```bash
   docker-compose run --rm app sh -c "yes | ./listmonk --install"
   ```

3. **Start the Service:**
   ```bash
   docker-compose up -d
   ```

4. **Access the Dashboard:**
   Navigate to `http://localhost:9000` and log in with the `ADMIN_USERNAME` and `ADMIN_PASSWORD` you set in your `.env` file.

## Connecting an SMTP Relay
To actually send emails, log in to the Listmonk dashboard, navigate to **Settings > SMTP**, and enter the credentials for your mail provider (e.g., SendGrid, Amazon SES, Mailgun, Postmark).
