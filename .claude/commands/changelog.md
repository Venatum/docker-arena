# /changelog

Generate a changelog from git history since the last tag.

## Steps

1. Find the last tag: `git describe --tags --abbrev=0`
2. Get commits since that tag: `git log <last-tag>..HEAD --oneline --no-merges`
3. Group commits by Conventional Commits type:
   - `feat` → Features
   - `fix` → Bug Fixes
   - `chore`, `ci`, `build` → Maintenance
   - `docs` → Documentation
   - `refactor`, `perf` → Improvements
   - `BREAKING CHANGE` → Breaking Changes (top priority)
4. Format as markdown changelog section

## Output format

```markdown
## [Unreleased] — since <last-tag>

### Breaking Changes
- ...

### Features
- ...

### Bug Fixes
- ...

### Maintenance
- ...
```

## Allowed tools
- Bash(git:*)
