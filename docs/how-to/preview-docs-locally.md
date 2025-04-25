# How to Preview Documentation Locally

Learn how to preview the Hedgehog documentation site on your local machine using the recommended, team-standard workflow. This guide covers all prerequisites, setup steps, and troubleshooting tips.

---

## Prerequisites

Before you can preview the documentation locally, ensure you have:

- **Docker** (or a compatible container engine) installed and running
- The [`just`](https://just.systems) command-line tool installed
- Access credentials for Hedgehog's [GitHub Container Registry (GHCR)](https://ghcr.io) (see [Download](../getting-started/download.md) for instructions)

> **Why Docker and GHCR?**
> The `just serve` command runs the documentation site inside a pre-built Docker container. This ensures your local preview matches the CI/CD and production environment exactly, avoiding dependency or version mismatches. The container image must be pulled from GHCR, so authentication is required.

---

## Step-by-Step: Previewing the Docs

1. **Authenticate with GHCR**
   - Follow the instructions on the [Download page](../getting-started/download.md) to obtain credentials and log in:
     ```bash
     docker login ghcr.io --username <your_username> --password <your_token>
     ```
2. **Start the local preview server**
   - In the `docs` directory, run:
     ```bash
     just serve
     ```
   - This will pull the latest Hedgehog docs container image and start a local MkDocs server at [http://localhost:8000](http://localhost:8000).
3. **Troubleshooting**
   - If you see an authentication error or `403 Forbidden`, ensure you are logged in to GHCR and your credentials are valid.
   - If you do not have Docker or just installed, follow the [installation instructions for Docker](https://docs.docker.com/get-docker/) and [`just`](https://just.systems/man/en/).
   - If you prefer or need to run MkDocs directly (not recommended), you can use:
     ```bash
     mkdocs serve
     ```
     Note: This may not match the team-standard environment.

---

## Related Information

- [Download page: Getting GHCR credentials](../getting-started/download.md)
- [Contributing guidelines](../contribute/overview.md)
- [MkDocs documentation](https://www.mkdocs.org/)

---

_Last updated: 2025-04-25_
