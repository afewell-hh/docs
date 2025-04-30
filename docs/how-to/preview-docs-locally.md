# How to Preview Documentation Locally

This guide explains how contributors can preview changes to the documentation on a local machine before submitting a pull request. It covers prerequisites, setup steps, serving the site, and troubleshooting.

---

## Prerequisites

- Git installed
- Python 3.8+ installed
- pip installed
- mkdocs and mkdocs-material packages installed
- A local clone of the githedgehog/docs repository

---

## Setup

1. Clone the repository:
   ```zsh
   git clone https://github.com/githedgehog/docs.git
   cd docs
   ```
2. Install dependencies:
   ```zsh
   pip install --upgrade pip
   pip install mkdocs mkdocs-material
   ```
3. Verify installation:
   ```zsh
   mkdocs --version
   ```

---

## Serving the Site

Run the local server:
```zsh
mkdocs serve
```
Open a browser at <http://localhost:8000>.
Press <kbd>Ctrl+C</kbd> to stop the server.

---

## Troubleshooting

- If port 8000 is in use, specify a different port:
  ```zsh
  mkdocs serve --dev-addr 127.0.0.1:9000
  ```
- If you encounter missing plugin errors, ensure mkdocs-material is installed.

---

## Related Links

- [Contributing to docs](../contribute/docs.md)
- [MkDocs documentation](https://www.mkdocs.org/)

_Last updated: 2025-04-29_
