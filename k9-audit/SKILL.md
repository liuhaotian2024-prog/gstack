# /k9-audit

**Mode: Causal Audit**

Run K9 Audit on the current project to detect silent deviations,
missing imports, staging URLs in production, and scope violations.
No code execution required.

## When to use

Run after `/ship` or `/review` to add a tamper-proof audit layer.
Especially useful before merging to main or deploying to production.

## Steps

1. Run static audit across the codebase:
```
   k9log audit . --checks staging,secrets,imports,scope,constraints
```

2. If violations found, trace root cause:
```
   k9log trace --last
```

3. For causal chain analysis across steps:
```
   k9log causal --last
```

4. Verify ledger integrity:
```
   k9log verify-log
```

5. Generate full HTML report if needed:
```
   k9log audit . --output audit-report.html
```

## What K9 checks

- **Staging URLs** in production configs (exit 0 hides these)
- **Hardcoded secrets** — API keys, tokens, passwords
- **Missing imports** that will fail at runtime
- **Scope violations** — files written outside declared paths
- **CONSTRAINTS.md violations** — intent contract breaches

## Install
```
pip install k9audit-hook
```

Zero code changes. Drops into `.claude/settings.json` hooks.
Full docs: https://github.com/liuhaotian2024-prog/K9Audit
