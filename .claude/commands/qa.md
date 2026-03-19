# /qa

Full quality check: code review.

## Steps

### 1. Analyze the diff

Run `git diff HEAD` (or `git diff master..HEAD` if on a feature branch).
Review the changes for:

- Correctness and logic errors
- Security issues (injection, hardcoded secrets, etc.)
- Project conventions: CommonJS, no TypeScript, npm only
- Code clarity and simplicity (no over-engineering)

### 2. Report

```
## QA Report

### Code Review
**Status**: ✅ PASS | ⚠️ WARNINGS | ❌ FAIL

#### Issues found
- [CRITICAL] ...
- [WARNING] ...
- [INFO] ...

### Verdict
✅ READY TO MERGE | ⚠️ MINOR ISSUES (can merge) | ❌ DO NOT MERGE
```

## Allowed tools

- Bash(git:\*)
- Bash(npm run:\*)
