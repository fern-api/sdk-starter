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

Generate production-ready SDKs in TypeScript, Python, Java, Ruby, C# and PHP in under 5 minutes using Fern.

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

### Step 4: Configure your SDK repositories

`fern/sdk-config.yml` has one target per language: Python, TypeScript, Java, Ruby, C# and PHP. Each target publishes its SDK in two steps:

1. **This repository generates.** A release workflow here runs `fern generate`. Fern commits the generated SDK to that language's own GitHub repository and creates a GitHub release.
2. **The SDK repository publishes.** Every generated SDK repository includes `.github/workflows/ci.yml`. When the release tag is pushed, it runs the tests and publishes the package to its registry.

For each language you want to ship:

1. Create a GitHub repository for the SDK and install the [Fern GitHub App](https://github.com/apps/fern-api) on it.
2. In `fern/sdk-config.yml`, set that target's `output.github.repository` to your repository and update its `package` name:

```yaml
targets:
  - language: python
    output:
      delivery: github
      github:
        repository: your-org/your-python-sdk-repo
        mode: release
```

3. Add the registry secrets to **the SDK repository** under **Settings > Secrets and variables > Actions**. The secret names match the `${...}` values in each target's `publish` block:

| Language   | Registry      | Secrets in the SDK repository                                                                                         |
| ---------- | ------------- | --------------------------------------------------------------------------------------------------------------------- |
| Python     | PyPI          | `PYPI_USERNAME` (set to `__token__`), `PYPI_PASSWORD` (a [PyPI API token](https://pypi.org/help/#apitoken))          |
| TypeScript | npm           | `NPM_TOKEN` (an [npm automation token](https://docs.npmjs.com/creating-and-viewing-access-tokens))                   |
| Java       | Maven Central | `MAVEN_USERNAME`, `MAVEN_PASSWORD` (a Central Portal user token), `MAVEN_SIGNATURE_KID`, `MAVEN_SIGNATURE_PASSWORD`, `MAVEN_SIGNATURE_SECRET_KEY` (your GPG signing key) |
| Ruby       | RubyGems      | `RUBYGEMS_API_KEY` (a [RubyGems API key](https://guides.rubygems.org/api-key-scopes/))                               |
| C#         | NuGet         | `NUGET_API_KEY` (a [NuGet API key](https://learn.microsoft.com/nuget/nuget-org/publish-a-package#create-an-api-key)) |
| PHP        | Packagist     | None. [Submit the SDK repository to Packagist](https://packagist.org/packages/submit) once; it picks up each release tag. |

4. Add one secret to **this repository**: `FERN_TOKEN`. Get it by running `fern token`. It is the only secret the release workflows here need.

To drop a language, delete its target from `fern/sdk-config.yml` and its workflow from `.github/workflows/`.

### Step 5: Release your SDKs

From the Actions tab of this repository, run the release workflow for a language (for example **Release Python SDK**) and enter a version. Each language has one: `python-sdk.yml`, `ts-sdk.yml`, `java-sdk.yml`, `ruby-sdk.yml`, `csharp-sdk.yml` and `php-sdk.yml`.

You can run the same thing locally from the root of the repository. It creates a real release, so the SDK repository will publish it:

```bash
fern generate --target python --version 1.0.0
```

If you just want to try the generated code, see [Preview an SDK locally](#preview-an-sdk-locally) instead.

## Preview an SDK locally

To try an SDK without pushing to GitHub or publishing, generate it into a local folder. You only need to be logged in to Fern. From the root of the repository, run:

```bash
fern generate --target <lang> --preview --output sdks/preview/<lang>
```

Replace `<lang>` with `python`, `typescript`, `java`, `ruby`, `csharp` or `php`. The SDK is written to a folder inside `sdks/preview/<lang>` (for example `sdks/preview/python/fern-python-sdk-0`).

## Customization Options

All SDK settings live in `fern/sdk-config.yml`, with one entry under `targets` per language. You can change package names, client names, publishing and more there. See the [SDK Config reference](https://buildwithfern.com/learn/sdks/reference/sdk-config) for every option.

---

## Support

Need help? [Set up a call](https://buildwithfern.com/contact) with an expert or email us at [support@buildwithfern.com](mailto:support@buildwithfern.com).
