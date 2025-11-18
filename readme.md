put this in .github/workflows/sbom.yml




name: SBOM Security Check

on:
  pull_request:
  push:

jobs:
  sbom:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: SBOM Scan
        uses: H-strangeone/sbom-tm-action@v1
        with:
          mode: auto
          project: myapp

      - name: Comment PR
        uses: marocchino/sticky-pull-request-comment@v2
        with:
          path: sbom-tm-report.md





recommended put this aswell but in root as .sbom-ci.yml

# SBOM-TM CI Policy Configuration

# -------------------------------------------
# Fail pipeline on these vulnerability severities
# -------------------------------------------
fail_on_severities:
  - CRITICAL
  - HIGH

# -------------------------------------------
# Fail pipeline when Rule Engine flags these categories
# -------------------------------------------
fail_on_rule_categories:
  - DEPRECATED
  - WEAK_CRYPTO
  - MISCONFIG
  - INSECURE_VERSION

# -------------------------------------------
# Minimum threat score (0–100)
# -------------------------------------------
min_threat_score: 60

# -------------------------------------------
# Ignore specific CVEs permanently (allowlisting)
# -------------------------------------------
ignore_cves:
  - "CVE-2023-9999"
  - "CVE-2020-12345"

# -------------------------------------------
# Ignore specific packages
# -------------------------------------------
ignore_packages:
  - "example-logger"
  - "left-pad"

# -------------------------------------------
# Allow transitive vulnerabilities?
# If false, ANY transitive vuln still fails.
# -------------------------------------------
allow_transitive: false
