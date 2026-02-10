# Release Process for noxtara/run

This is the GitHub Action repository for running Noxtara scans.

## Repository Structure

- `action.yml` - GitHub Action definition
- `package.json` - NPM package metadata
- `README.md` - Public documentation

## Release Process

### Versioning

We use semantic versioning (MAJOR.MINOR.PATCH) but only expose MAJOR version via tags.

### Creating a Release

1. Make changes to `action.yml` or documentation
2. Commit changes to `main` branch
3. Create/update version tag:
   ```bash
   # For major version v1
   git tag -fa v1 -m "Update v1 to latest"
   git push origin v1 --force
   ```

### Tag Strategy

- `v1` - Points to latest v1.x.x (moving tag)
- Consumers use `noxtara/run@v1` to always get latest v1
- Force push the tag to update it after commits

### Testing

Before releasing:
1. Test the action in a separate repository
2. Verify inputs work correctly
3. Check that env vars are passed properly

## Git Submodules

This repository is included as a git submodule in the main CLI repository at:
- Path: `.context/run/`
- URL: https://github.com/noxtara/run

When making changes:
1. Edit in the submodule directory (`.context/run/`)
2. Commit and push from there
3. Update the submodule reference in the main repo
