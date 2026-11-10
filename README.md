## DevSecOps notes

- **Secrets:** never store them in code or Git; inject them at run time (Kubernetes Secret mounted as a file).
- **Scanning:** Trivy scans secrets, Dockerfiles and images; Checkov scans Terraform.
- **Security gates:** `--exit-code 1` makes the pipeline fail on findings.
- **Non-root:** `USER appuser` in the Dockerfile.
- **NetworkPolicy:** only the `api` pod may reach the `db` pod.
- **Signing:** Cosign signs the image after all scans pass.
- **Deliverables:** pipeline in `.github/workflows/pipeline.yml`, `THREAT_MODEL.md`, `REMEDIATION_REPORT.md`.
