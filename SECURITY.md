# Security Policy

This repository contains Linux/Ubuntu client release documentation for VLF.

A formal independent third-party security audit has not yet been completed. Responsible disclosure is welcome.

## Supported Versions and Branches

| Branch or version | Status |
| --- | --- |
| `main` | Documentation/release metadata support |
| Latest Ubuntu/Linux release | Supported for user-facing security reports |
| Older releases | Best-effort only |

TODO: define exact supported Linux release versions.

## Reporting a Vulnerability

- Security contact: TODO: add public security contact
- Include distro version, package version, installation mode and reproduction steps.
- Redact subscription links, profile credentials, logs, generated configs and private domains.

## Scope

In scope:

- Published Linux/Ubuntu package behavior described in README.
- TUN privilege bootstrap, polkit/udev/NetworkManager integration described by README.
- User-facing sing-box/Xray client behavior reproducible in released packages.

Out of scope unless tied to a released VLF build:

- social engineering;
- attacks against Linux distributions, package mirrors or third-party VPN providers.

## Safe Harbor

Good-faith testing is welcome when it uses your own machine and synthetic profiles.
