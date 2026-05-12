# Architecture

This repository documents the Linux/Ubuntu VLF client release.

A formal independent third-party security audit has not yet been completed.

The README describes a sing-box-based Linux VPN client supporting VLESS/Reality/Hysteria2/Trojan/VMess, TUN mode and RU/GLOBAL routing. It also describes `.deb` packaging, capabilities, polkit, udev and NetworkManager integration.

## Security Boundaries

- User-provided profile/subscription config.
- Local generated engine configs and logs.
- Linux TUN/capability boundary.
- polkit/udev/NetworkManager package integration.
- Release package and bundled engine artifacts.

## Known Limitations

- This repository is documentation/release oriented.
- Full implementation details require review of the source repository and package contents.
- Formal external audit is not completed yet.
