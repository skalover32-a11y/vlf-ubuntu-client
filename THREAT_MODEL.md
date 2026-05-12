# Threat Model

A formal independent third-party security audit has not yet been completed.

## Assets

- VPN profile credentials and subscription links.
- Local generated engine configs.
- Runtime logs.
- Linux TUN permissions/capabilities.
- Package scripts and release artifacts.

## Threats

- Credential leakage through logs/configs.
- Malicious subscription/profile input.
- Overbroad polkit/capability permissions.
- Package or bundled binary compromise.
- Local attacker reading client files.

## Recommended Improvements

- Publish package checksums and source commit provenance.
- Document local storage paths and log redaction behavior.
- Review polkit/capability scope for least privilege.
- Add public security contact.

## Non-Goals

- Full source audit from this repository alone.
- DDoS mitigation.
- Service-level retention policy.
