# Homelab Blog: Hugo Source & CI/CD

This repository contains the source code for my personal blog, which is built with Hugo and hosted entirely on my homelab infrastructure. It's the content layer that sits on top of the infrastructure provisioned by the homelab-iac repo and the applications deployed by the homelab-gitops repo.

The live site can be viewed at: **https://hugo.milenika.dev**

## CI/CD Workflow 

This repository features a fully automated CI/CD pipeline using **GitHub Actions**. When a change is pushed to the `main` branch, the following process is triggered:

1. **Build**: The GitHub Actions workflow checks out the code and uses the `peaceiris/actions-hugo` action to build the static site.
2. **Sync to MinIO**: The workflow then uses the MinIO Client (`mc`) to sync the contents of the generated `public/` directory to the `hugo-static` bucket in my homelab's MinIO instance.
3. **Purge Cache**: Finally, the workflow makes an API call to Cloudflare to purge the cache, ensuring visitors see the latest version of the site immediately.

The static content is served to the public by an **NGINX** server (running in Kubernetes) that is configured to act as a reverse proxy for the MinIO bucket.

## Local Development 

To write new posts or test changes locally, you can run the Hugo development server on your machine.

**Prerequisites**:
- You must have the **extended version** of Hugo installed.
- You need to have the `PaperMod` theme installed as a submodule.

**Steps**:

1. Clone the repository:

```bash
git clone https://github.com/mikha-22/hugo-site.git
cd hugo-site
```

2. Initialize the theme submodule:

```bash
git submodule update --init --recursive
```

3. Run the local development server:

```bash
hugo server -D
```

The `-D` flag builds and serves draft posts as well. You can now access the site locally at `http://localhost:1313`.

## Configuration

- **Site Configuration**: The main settings, including the site title, menu, and theme options, are located in `config.yaml`.
- **Content**: All blog posts and pages are written in Markdown and live in the `content/` directory.

## Pipeline Secrets

The GitHub Actions workflow in `.github/workflows/deploy.yaml` relies on the following secrets being configured in the repository's settings (`Settings > Secrets and variables > Actions`):

- `MINIO_ACCESS_KEY`: The access key for the MinIO user.
- `MINIO_SECRET_KEY`: The secret key for the MinIO user.
- `CLOUDFLARE_API_TOKEN`: A Cloudflare API token with permission to purge the cache.
- `CLOUDFLARE_ZONE_ID`: The ID of the Cloudflare zone that corresponds to the `milenika.dev` domain.
