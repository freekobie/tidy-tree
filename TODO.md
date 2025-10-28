# Tidy Tree — File System Cleaner & Organizer (Go CLI)

A fast, safe, and configurable CLI tool written in Go for cleaning up cluttered file systems and organizing files automatically.
The tool's command is `tdt`.

---

## Project Overview

**Goal:**
Create a cross-platform CLI utility that:

- Scans directories for unused or duplicate files
- Organizes files by type/date
- Cleans up empty or redundant folders
- Offers dry-run previews and smart configuration options

---

## TODO LIST

### Project Setup

### Core Features

#### Directory Scanning

- [ ] Recursively scan directories
- [ ] Collect metadata (path, size, type, modified time)
- [ ] Identify:

  - [ ] Duplicate files (hash comparison)
  - [ ] Empty folders
  - [ ] Large or old files

- [ ] Generate summary reports
- [ ] Optionally export results (JSON/CSV)

#### File Organization

- [ ] Organize files by:

  - [ ] File type (`Documents`, `Images`, `Music`, etc.)
  - [ ] Modified date (`Year/Month`)
  - [ ] Custom user rules

- [ ] Preserve directory structure optionally
- [ ] Handle name collisions safely
- [ ] Support dry-run preview before moving files

#### File Cleanup

- [ ] Remove empty folders
- [ ] Delete duplicates safely
- [ ] Delete temporary or cache files (`*.tmp`, `*.bak`)
- [ ] Delete files older than N days
- [ ] Move deleted files to Trash (optional, cross-platform)

---

### Configuration System

- [ ] Support configuration file: `~/.config/tdt/config.yaml`
- [ ] Support per-project `.tdt.yaml`
- [ ] Merge config with environment variables and CLI flags
- [ ] Example config:

  ```yaml
  organize:
    by: "type"
    target_dir: "~/Organized"

  cleanup:
    delete_empty: true
    remove_duplicates: true
    max_age_days: 90

  exclude:
    - "*.git*"
    - "node_modules"
  ```

---

### Command-Line Interface

- [ ] Use [Cobra](https://github.com/spf13/cobra)
- [ ] Binary name: `tdt`
- [ ] Commands:

  - [ ] `tdt scan [path]` — Analyze directory and print summary
  - [ ] `tdt organize [path]` — Organize files according to rules
  - [ ] `tdt clean [path]` — Clean duplicates, temp files, and empty dirs
  - [ ] `tdt config` — View or edit configuration
  - [ ] `tdt version` — Display version info

- [ ] Global flags:

  - [ ] `--config <file>`
  - [ ] `--dry-run`
  - [ ] `--verbose`
  - [ ] `--path <dir>`

---

### Smart Rules System

- [ ] Implement pattern-based rules:

  ```yaml
  rules:
    - match: "*.mp3"
      move_to: "~/Music"
    - match: "*.zip"
      move_to: "~/Archives"
  ```

- [ ] Auto-detect file types via MIME
- [ ] Hash-based duplicate detection (SHA256)
- [ ] Smart skip logic for system/protected folders

---

### CLI UX

- [ ] Interactive confirmation prompts
- [ ] Progress bars during long operations
- [ ] Colored output for clarity
- [ ] Summary report example:

  ```bash
  234 files organized
  19 duplicates removed
  12 empty folders deleted
  Completed in 2.4s
  ```

- [ ] Quiet mode (`--quiet`)
- [ ] JSON output (`--json`) for automation

---

### File Operations

- [ ] Safe atomic move/copy
- [ ] Preserve permissions and timestamps
- [ ] Cross-platform path handling
- [ ] Retry or skip locked files gracefully

---

### Testing & Quality

- [ ] Unit tests for each package
- [ ] Integration tests for filesystem operations
- [ ] Use temporary directories for testing (`os.MkdirTemp`)
- [ ] Add `golangci-lint` for linting
- [ ] GitHub Actions CI setup
- [ ] Benchmark scanning and organizing performance

---

### Distribution

- [ ] Build cross-platform binaries (`goreleaser`)
- [ ] Output to `dist/tdt_<os>_<arch>.tar.gz`
- [ ] Homebrew tap for macOS users
- [ ] `go install github.com/freekobie/tidy-tree/cmd/tdt@latest`
- [ ] Version tagging and changelog

---

### Future Enhancements

- [ ] Watch mode for real-time auto-organization
- [ ] Cron-like scheduled cleanup
- [ ] GUI dashboard (optional future project)
- [ ] Plugin system for custom rules
- [ ] Cloud integration (Dropbox, Google Drive, S3)

---

## Example Usage

```bash
# Scan and preview changes
tdt scan ~/Downloads --dry-run

# Organize by file type
tdt organize ~/Downloads --by type

# Clean duplicates and empty folders
tdt clean ~/Documents --remove-duplicates --delete-empty

# Use custom config
tdt organize --config ~/.config/tdt/work.yaml
```

---
