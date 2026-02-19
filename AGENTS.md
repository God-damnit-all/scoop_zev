# QWEN.md – Zev Scoop Bucket

## Project Overview

**Zev** is a custom [Scoop](https://scoop.sh/) bucket—a curated collection of application manifests (JSON files) for use with the Windows package manager Scoop. This repository enables streamlined, scriptable installation and management of Windows software via `scoop`, focusing on providing additional, niche, or specialized packages beyond those available in the main Scoop buckets.

- **Type**: Code Project / Package Repository
- **Technologies**: PowerShell, JSON
- **Primary Structure:**
  - `bucket/` – Application manifests (`*.json`) defining installable packages
  - `bin/` – PowerShell scripts for formatting, testing, validating, and checking manifests
  - `scripts/` – Supporting schema and subdirectories (e.g., `neovim`)
  - `.github/` – GitHub meta (templates, workflows, ownership)
  - `.vscode/` – Editor and tooling recommendations/settings

## Building, Testing & Maintenance

### Validating and Formatting
- **Format JSON Manifests:**
  ```powershell
  bin/formatjson.ps1
  ```
  Runs formatting on all manifests in `bucket/` using Scoop's standard formatting logic.

### Manifest Version Checking
- **Check for Manifest Updates:**
  ```powershell
  bin/checkver.ps1
  ```
  Checks all manifests in `bucket/` for available upstream updates.

### Testing
- **Pester Unit Tests:**
  ```powershell
  bin/test.ps1
  ```
  Runs [Pester](https://github.com/pester/Pester) PowerShell-based tests on bucket scripts and logic. Requires PowerShell 5.1+ and Pester >= 5.2.0.
- **Import Bucket Tests:**
  ```powershell
  Scoop-Bucket.Tests.ps1
  ```
  Sources and runs Scoop's bucket-level test suite (automated validation for manifests via Scoop infrastructure).

### General Bucket Maintenance
- Ensure all manifests conform to schema:
  - Bucket schema: `scripts/schema.json`
  - VSCode uses schema for live validation (see `.vscode/settings.json`)
- All JSON in `bucket/` should validate against [Scoop's bucket schema](https://raw.githubusercontent.com/ScoopInstaller/scoop/refs/heads/master/schema.json).

## Development Conventions

### Style & Formatting
- **EditorConfig:** Enforces UTF-8 charset, CRLF EOL, 4-space indentation, trimming trailing whitespace, and newline at file end (see `.editorconfig`).
- **Git Attributes:** All text files normalized to CRLF in working tree, LF in repository (`.gitattributes`).
- **Markdown:** Markdownlint disables MD013 (line length), and tunes MD024 (siblings-only heading collision).
- **Recommended Tools:**
  - VSCode with EditorConfig and PowerShell extensions (`.vscode/extensions.json`).

### Contribution Guidelines
- Use conventional PR title: `<manifest-name[@version]|chore>: <general summary of the pull request>`
- Open relevant issue before new PR
- Follow [ScoopInstaller contributing guide](https://github.com/ScoopInstaller/.github/blob/main/.github/CONTRIBUTING.md)
- See `.github/pull_request_template.md` for PR requirements.
- `.github/CODEOWNERS` enforces workflow ownership by ScoopInstaller maintainers.

### Script Analysis & Formatting
- PowerShell scripts use OTBS preset, align property-value pairs, and ignore one-line blocks (`.vscode/settings.json`).

## Usage Notes

- **Add this bucket:**
  ```powershell
  scoop bucket add zev https://github.com/<user>/zev
  ```
- **Install packages:**
  ```powershell
  scoop install <package-name>
  ```
- **Validate or update manifests:**
  Use provided scripts in `bin/` to check, update, and format manifests before submitting PRs.

## Licensing

- **License:** Public Domain / [Unlicense](http://unlicense.org/)

## TODOs
- Ensure all new manifests comply with latest schema (`scripts/schema.json`).
- Document any bucket-specific scripts placed in `scripts/` and subfolders.
- Add more automated tests if bucket logic/scripts become more complex.

---
