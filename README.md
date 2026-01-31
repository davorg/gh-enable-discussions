# gh-enable-discussions

Enable GitHub Discussions across **all repositories** owned by a user or organisation.

This is a small wrapper around the GitHub CLI (`gh`) that:

* iterates through repos for an owner
* enables Discussions where you have permission
* optionally performs a dry run
* optionally checks each repo first and only changes those currently disabled

---

## Requirements

* GitHub CLI: `gh`
* An authenticated `gh` session with sufficient permissions for the target repos

Check you’re logged in:

```
gh auth status
```

---

## Installation

Clone the repository and make the script executable:

```
git clone <REPO_URL>
cd gh-enable-discussions
chmod +x gh-enable-discussions
```

Optionally install it somewhere on your `PATH`:

```
sudo cp gh-enable-discussions /usr/local/bin/
```

---

## Usage

### Enable discussions everywhere you can administer

```
gh-enable-discussions --owner my-org
```

### Dry run (no changes made)

```
gh-enable-discussions --owner my-org --dry-run
```

### Only enable when currently disabled

This avoids unnecessary API calls.

```
gh-enable-discussions --owner my-org --only-when-disabled
```

### Recommended first run

```
gh-enable-discussions --owner my-org --dry-run --only-when-disabled
```

### Increase repository limit

(Default is 2000.)

```
gh-enable-discussions --owner my-org --limit 5000
```

---

## Exit codes

* `0` — success
* `1` — one or more repositories failed to update, or no repositories found
* `2` — invalid arguments
* `127` — missing dependency (for example, `gh`)

---

## Notes

* `--owner` may be either a **user** or an **organisation**.
* The script only affects repositories where the authenticated user has admin permission.
* When `--only-when-disabled` is enabled, the script queries the repository state before attempting changes.

---

## Development

### Linting

This project uses **ShellCheck** to catch common shell scripting errors.

Run locally:

```
shellcheck gh-enable-discussions
```

ShellCheck is also run automatically in GitHub Actions on pushes and pull requests.

---

## Licence

MIT — see `LICENSE`.

