# Mintlify Preview GitHub Action 🚀

This GitHub Action automates the process of deploying a **Mintlify preview** for documentation updates when a pull
request is opened or updated. It posts a comment on the pull request with a link to the preview deployment.

## Usage

To use this action, add the following workflow to your repository (`.github/workflows/mintlify-preview.yml`):

```yaml
name: Mintlify Preview

on:
  pull_request:
    paths:
      - 'docs/**'  # Trigger only for changes in the docs directory
    types:
      - opened
      - synchronize

jobs:
  preview:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Deploy Mintlify Preview
        uses: frain-dev/mintlify-preview-action@v0.1.0
        with:
          docs_path: "docs/mint.json"  # Path to your documentation file
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

The action accepts the following inputs:

| Input Name     | Description                                             | Required | Default Value                                    |
|----------------|---------------------------------------------------------|----------|--------------------------------------------------|
| `docs_path`    | Path to the documentation file (e.g., `docs/mint.json`) | Yes      | None                                             |
| `backend_url`  | Custom backend server for deployment (optional)         | No       | `https://mintlify-previewer.getconvoy.io/deploy` |
| `github_token` | GitHub token to comment on the PR                       | Yes      | None                                             |

## Outputs

The action provides the following output:

| Output Name      | Description                     |
|------------------|---------------------------------|
| `deployment_url` | The URL of the Mintlify preview |

## Branding

- **Icon**: `upload-cloud`
- **Color**: `blue`

## How It Works

1. The action triggers on pull requests that modify files in the `docs/` directory.
2. It sends a request to the Mintlify previewer backend with the pull request details and documentation path.
3. The backend generates a preview deployment and returns the deployment URL.
4. The action posts a comment on the pull request with the preview URL.

## Example

Here’s an example of the comment posted on the pull request:

```
🚀 Mintlify preview available at: https://01JMCNA4MFFE1PHTSHJ46JV8CG.mintlify-previewer.getconvoy.io
```

## License

This project is licensed under the [MIT License](LICENSE).

---

Made with ❤️ by [frain-dev](https://github.com/frain-dev)