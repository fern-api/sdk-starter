<br/>
<div align="center">
  <a href="https://www.buildwithfern.com/?utm_source=github&utm_medium=readme&utm_campaign=fern&utm_content=logo">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="/fern/docs/assets/fern-logo-white.svg">
      <source media="(prefers-color-scheme: light)" srcset="/fern/docs/assets/fern-logo-primary.svg">
      <img alt="logo" src="/fern/docs/assets/fern-logo-primary.svg" height="50" align="center">
    </picture>
  </a>
  
  <br/>

# SDK Starter

Generate production-ready TypeScript and Python SDKs in under 5 minutes using Fern.

</div>

## Customer Showcase

Get inspired by SDKs built with Fern: [Merge](https://github.com/merge-api/merge-node-client) | [Square](https://github.com/square/square-go-sdk) | [ElevenLabs](https://github.com/elevenlabs/elevenlabs-python) | [Flatfile](https://github.com/FlatFilers/flatfile-node) |

---

## Requirements

- Node 18 or higher
- A [GitHub](https://github.com) account
- The [Fern GitHub App](https://github.com/apps/fern-api) installed

### Step 1: Use this template

1. Click on the **Use this template** button (found at the top right of this page). You must be logged into GitHub.
2. Choose the option to **create a new repository**. Name it whatever you'd like.

### Step 2: Clone and configure the repo

1. Clone your newly created repository and open it in your favorite code editor (e.g., VS Code).
2. Open `fern/fern.config.json` and update the `organization` field with your organization name. Keep the pinned `version`.

```json
{
  "organization": "your-organization-name",
  "version": "5.228.1"
}
```

3. Open `fern/sdk-config.yml` and change `sdkName` to your organization or product name.

```yaml
sdkName: your-sdk-name
```

### Step 3: Install and configure Fern

1. Install the Fern CLI globally:

```bash
npm install -g fern-api
```

2. Log in to Fern:

```bash
fern login
```

### Step 4: Configure your SDK settings

The repository comes pre-configured for TypeScript and Python SDK generation in `fern/sdk-config.yml`. You'll need to:

1. Create a GitHub repository for each SDK you want to generate.
2. Install the [Fern GitHub App](https://github.com/apps/fern-api) in each of those repositories.
3. In `fern/sdk-config.yml`, set `output.github.repository` on the `python` and `typescript` targets to your repositories:

```yaml
targets:
  - language: python
    output:
      delivery: github
      github:
        repository: your-org/your-python-sdk-repo

  - language: typescript
    output:
      delivery: github
      github:
        repository: your-org/your-ts-sdk-repo
```

4. Add these secrets to your template repository under **Settings > Secrets and variables > Actions**. The release workflows in `.github/workflows/` read them.

| Secret       | Where to get it                                                                                   |
| ------------ | ------------------------------------------------------------------------------------------------- |
| `FERN_TOKEN` | Run `fern token`                                                                                  |
| `PYPI_TOKEN` | Create an [API token](https://pypi.org/help/#apitoken) in your PyPI account settings              |
| `NPM_TOKEN`  | Create an [automation token](https://docs.npmjs.com/creating-and-viewing-access-tokens) on npm    |

### Step 5: Generate your SDKs

Running these commands publishes a real release: the SDK is pushed to your GitHub repository and published to PyPI (Python) or npm (TypeScript). `fern/sdk-config.yml` reads the registry tokens from your environment, so export them in your shell first:

```bash
export PYPI_TOKEN=your-pypi-token
export NPM_TOKEN=your-npm-token
```

If you just want to try the generated code, see [Preview an SDK locally](#preview-an-sdk-locally) instead.

To generate and publish your SDKs, run these from the root of the repository:

```bash
fern generate --target python
```

AND

```bash
fern generate --target typescript
```

The generated SDKs will be:

- Committed to your specified GitHub repositories
- Published to npm (TypeScript) and PyPI (Python) if configured
- Version-controlled using semantic versioning

To release from CI instead, run the **Release Python SDK** or **Release TypeScript SDK** workflow from the Actions tab and enter a version.

## Preview an SDK locally

To try an SDK without pushing to GitHub or publishing, generate it into a local folder. You only need to be logged in to Fern. From the root of the repository, change into the `fern` folder and run:

```bash
cd fern
fern generate --target <lang> --preview --output ../sdks/preview/<lang>
```

Replace `<lang>` with `python`, `typescript`, `java`, `ruby`, `csharp` or `php`. The SDK is written to `sdks/preview/<lang>` at the repository root.

## Customization Options

All SDK settings live in `fern/sdk-config.yml`, with one entry under `targets` per language. Besides Python and TypeScript, the starter configures Java, Ruby, C# and PHP. Those four write to `sdks/<lang>` on your machine when you run `fern generate --target <lang>`.

You can modify these settings or add more options by editing `fern/sdk-config.yml`. See the [SDK Config reference](https://buildwithfern.com/learn/sdks/reference/sdk-config) for every option.

---

## Support

Need help? [Set up a call](https://buildwithfern.com/contact) with an expert or email us at [support@buildwithfern.com](mailto:support@buildwithfern.com).
