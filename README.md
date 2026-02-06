# Run Noxtara Scan

GitHub Action to run SCA/SAST security scans using the Noxtara CLI.

## Usage

```yaml
name: Security Scan
on: [push, pull_request]

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: xcidic/noxtara-action@v1
        with:
          api-key: ${{ secrets.NOXTARA_API_KEY }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api-key` | Noxtara API key | Yes | - |
| `api-url` | Noxtara API URL | No | `https://app.noxtara.com/api/main/client` |
| `working-directory` | Directory to scan | No | `.` |
| `cli-version` | CLI version | No | `latest` |

## Configuration

Scan options (include patterns, ignore patterns, format, scan name) should be configured in a `noxtara.yaml` file in your repository root. The action will automatically read these settings.

### Example noxtara.yaml

```yaml
scan:
  scaSast:
    from: .
    name: "My Project Security Scan"
    include:
      - src/**
      - lib/**
    ignore:
      - "**/node_modules/**"
      - "**/*.test.ts"
      - "dist/**"
    format: zip
```

## Examples

### Basic

```yaml
- uses: xcidic/noxtara-action@v1
  with:
    api-key: ${{ secrets.NOXTARA_API_KEY }}
```

### With custom working directory

```yaml
- uses: xcidic/noxtara-action@v1
  with:
    api-key: ${{ secrets.NOXTARA_API_KEY }}
    working-directory: ./src
```

## Requirements

You need a Noxtara API key to use this action. Set it as a repository secret:

1. Go to your repository Settings
2. Navigate to Secrets and variables > Actions
3. Click "New repository secret"
4. Name: `NOXTARA_API_KEY`
5. Value: Your Noxtara API key

## License

MIT
