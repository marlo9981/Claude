# CLAUDE.md

This file provides guidance for AI assistants (Claude and others) working within this repository.

---

## Repository Overview

**Repository:** `marlo9981/Claude`
**Branch convention:** Feature branches use the prefix `claude/` followed by a descriptive slug and session ID (e.g., `claude/add-claude-documentation-IGo5i`).

This is a newly initialized repository. As content is added, update this file to reflect the actual structure, workflows, and conventions used.

---

## Development Workflow

### Branch Strategy

- **Never push directly to `main` or `master`.**
- All work happens on feature branches named `claude/<description>-<session-id>`.
- Open pull requests to merge feature branches into the default branch.

### Commit Conventions

Use clear, imperative commit messages:

```
Add user authentication module
Fix null pointer in payment processor
Refactor database connection pooling
Update CLAUDE.md with project structure
```

- Keep subject line under 72 characters.
- Use the body to explain *why*, not *what* (the diff shows what changed).
- Reference issue numbers where applicable: `Fixes #42`.

### Git Push Workflow

Always push with the upstream tracking flag:

```bash
git push -u origin <branch-name>
```

On network failure, retry with exponential backoff: 2s → 4s → 8s → 16s (max 4 retries).

---

## Project Structure

> This section will be updated as the project grows. Below is the expected canonical layout.

```
/
├── CLAUDE.md              # AI assistant guidance (this file)
├── README.md              # Human-facing project documentation
├── .github/
│   └── workflows/         # CI/CD pipeline definitions
├── src/                   # Primary source code
├── tests/                 # Test suite
├── docs/                  # Extended documentation
└── scripts/               # Utility and build scripts
```

---

## Key Conventions for AI Assistants

### Reading Before Editing

Always read a file before modifying it. Never guess at file contents or structure.

```
Read → Understand → Edit
```

### Minimal, Focused Changes

- Make only the changes requested or clearly necessary.
- Do not refactor surrounding code, add comments, or improve style unless explicitly asked.
- Do not add error handling for scenarios that cannot happen.
- Do not introduce abstractions for one-time operations.

### Security

Never introduce:
- SQL injection vulnerabilities
- Command injection (unsanitized shell input)
- Cross-site scripting (XSS)
- Hardcoded secrets, API keys, or credentials
- Insecure deserialization

Validate input only at system boundaries (user input, external APIs). Trust internal framework guarantees.

### No Speculative Features

Do not add:
- Features not requested
- Extra configurability
- Future-proofing abstractions
- Docstrings or type annotations on unchanged code
- Backwards-compatibility shims for removed code

### File Management

- Prefer editing existing files over creating new ones.
- Do not create `*.md` documentation files unless explicitly requested.
- Do not create helper utilities for one-time operations.

---

## Testing

> Update this section once a testing framework is established.

**Guiding principles:**
- Run tests before pushing.
- All new features must include corresponding tests.
- Tests should be co-located with source code or in a top-level `tests/` directory.

Common test commands (update once framework is chosen):

```bash
# Example for Node.js projects
npm test

# Example for Python projects
pytest

# Example for Go projects
go test ./...

# Example for Rust projects
cargo test
```

---

## Linting and Formatting

> Update this section once linters and formatters are configured.

**Guiding principles:**
- Never skip linting hooks (`--no-verify`).
- Fix lint errors before committing.
- Format code consistently with the project's configured formatter.

---

## CI/CD

> Update this section once `.github/workflows/` is populated.

**Guiding principles:**
- All CI checks must pass before merging a pull request.
- Do not bypass CI with `[skip ci]` tags unless absolutely necessary and approved.
- If a pre-commit hook fails, fix the underlying issue — do not amend or force-push around it.

---

## Pull Requests

When creating a pull request:

1. Keep the title concise (under 70 characters).
2. Include a summary of what changed and why.
3. Include a test plan describing how to verify the changes.
4. Reference any related issues.

Template:

```markdown
## Summary
- <bullet points describing changes>

## Test plan
- [ ] Describe manual or automated test steps
- [ ] Verify existing tests pass
```

---

## Environment and Tooling

- **Platform:** Linux
- **Shell:** bash/zsh
- **Current date context:** Update as needed — AI assistants should not assume the current date.

---

## Updating This File

This file should be kept current. When the project evolves (new dependencies, new structure, new workflows), update the relevant sections of this file so future AI sessions have accurate context.

Key triggers for updating `CLAUDE.md`:
- Adding a new top-level directory with distinct purpose
- Adopting a new testing framework or linter
- Changing the branching strategy
- Adding CI/CD pipelines
- Establishing new code style conventions
