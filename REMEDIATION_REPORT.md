# Remediation Report: secure-pipeline

## Findings and fixes

| # | Finding | Tool | Severity | Status | Fix |
|---|---------|------|----------|--------|-----|
| 1 | nginx:1.19 image has 42 Critical vulnerabilities | Trivy | Critical | Not fixed (practice image) | Use a newer image like nginx:1.27 |
| 2 | SSH port 22 open to 0.0.0.0/0 (CKV_AWS_24) | Checkov | High | Not fixed (practice file) | Change to a trusted IP only |
| 3 | GitHub token hard-coded in app.py | Trivy | Critical | Fixed | Read from environment variables |
| 4 | Missing HEALTHCHECK in Dockerfile (DS-0026) | Trivy | Low | Fixed | Added HEALTHCHECK line |
| 5 | Pods could all talk to the db pod | Manual test | Medium | Fixed | NetworkPolicy allows only api pod |

## Final result
CI pipeline passes with all security gates: secret scan, Dockerfile scan, image scan.
