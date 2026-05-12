# Audit Status

A formal independent third-party security audit has not yet been completed.

This repository has not completed a formal independent third-party security audit. Audit readiness depends on package provenance, source commit mapping and release artifact checks.

## Review Checklist

- [ ] Link Linux packages to source commits.
- [ ] Verify package checksums and signing process.
- [ ] Review sing-box/Xray artifact provenance.
- [ ] Review `CAP_NET_ADMIN`/`CAP_NET_RAW` handling.
- [ ] Review polkit rule scope.
- [ ] Review udev and NetworkManager integration.
- [ ] Review log redaction and generated config handling.

TODO: identify the source repository/commit for each public Linux release.
