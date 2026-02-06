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
| `name` | Scan entry name | No | Auto-generated |
| `include` | Glob patterns to include files (one per line) | No | - |
| `ignore` | Glob patterns to ignore (one per line) | No | - |
| `format` | Archive format: zip or tar-gzip | No | `zip` |

## Examples

### Basic

```yaml
- uses: xcidic/noxtara-action@v1
  with:
    api-key: ${{ secrets.NOXTARA_API_KEY }}
```

### With ignore patterns

```yaml
- uses: xcidic/noxtara-action@v1
  with:
    api-key: ${{ secrets.NOXTARA_API_KEY }}
    ignore: |
      **/node_modules/**
      **/*.test.ts
      dist/**
```

### With include patterns

```yaml
- uses: xcidic/noxtara-action@v1
  with:
    api-key: ${{ secrets.NOXTARA_API_KEY }}
    include: |
      src/**
      lib/**
    ignore: |
      **/*.test.ts
```

### Custom scan configuration

```yaml
- uses: xcidic/noxtara-action@v1
  with:
    api-key: ${{ secrets.NOXTARA_API_KEY }}
    name: "My Project Security Scan"
    working-directory: ./src
    format: tar-gzip
    include: |
      src/**
      lib/**
    ignore: |
      **/vendor/**
      **/*.spec.js
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
