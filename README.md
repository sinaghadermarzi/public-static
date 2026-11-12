# public-static

A static website served by nginx, deployed as a CapRover app.

- `site/` – the static files (HTML/CSS/JS/images) served at `/`
- `nginx.conf` – nginx server config (gzip, caching, `/healthz`, custom 404)
- `Dockerfile` + `captain-definition` – CapRover build

## Deploy

Every push to `main` runs `.github/workflows/deploy.yml`, which tars the repo
and deploys it to CapRover (it can also be run manually from the Actions tab).

One-time setup:

1. In CapRover, create an app (e.g. `public-static`). Container HTTP port is `80` (the default).
2. In the app's **Deployment** tab, enable **App Token** and copy it.
3. Add these GitHub repository secrets in this repo:
   - `CAPROVER_SERVER` – e.g. `https://captain.yourdomain.com`
   - `CAPROVER_APP` – the app name
   - `CAPROVER_TOKEN` – the app token

## Run locally

```bash
docker build -t public-static . && docker run --rm -p 8080:80 public-static
```

Then open http://localhost:8080.
