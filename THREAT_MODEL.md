# Threat Model: secure-pipeline

## What we protect
- Source code (GitHub repo)
- Docker image (secure-app)
- Secrets (passwords, tokens)
- Running app (Flask on port 5000)


## Threats and fixes

| # | Threat | What could happen | Our fix |
|---|--------|-------------------|---------|
| 1 | Hard-coded secret in code | Anyone with repo access can steal it | Trivy secret scan in the pipeline fails the build |
| 2 | Vulnerable library or base image | Attacker uses a known CVE to break in | Trivy image scan fails on Critical issues; versions pinned in requirements.txt |
| 3 | Container running as root | Attacker gets full power inside the container | `USER appuser` in the Dockerfile; Trivy config scan checks it |
| 4 | Insecure Dockerfile settings | Weak setup goes to production | Trivy config scan fails the build (found and fixed the missing HEALTHCHECK) |
| 5 | Tampered or fake image | A changed image gets deployed | Image signing with Cosign (not added yet) |
| 6 | Pod talking to anything in Kubernetes | Attacker moves from one pod to another | NetworkPolicy allows only needed traffic (Hands-on 6) |
| 7 | Secret leaked through env variables or logs | Attacker reads the password | Secret mounted as a file from a Kubernetes Secret (Hands-on 7) |
