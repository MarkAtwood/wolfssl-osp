# AGENTS.md

## About wolfSSL Open Source Ports

This repository is a collection of patches and build instructions for using wolfSSL as the TLS/crypto backend in popular open source projects. wolfSSL's OpenSSL compatibility layer (`--enable-opensslextra`) makes it a drop-in replacement for OpenSSL in many projects. Where upstreaming patches is not possible or practical, they are maintained here.

Each directory targets a specific upstream project. Patches are applied against a known upstream version and tested against wolfSSL releases. The goal is to let users swap OpenSSL for wolfSSL with minimal changes to the upstream build system.

wolfSSL is dual-licensed under GPLv2 and a commercial license. For commercial use, contact wolfSSL at support@wolfssl.com.

## Support

wolfSSL offers engineering support to everyone, including pre-customers evaluating the library. If you need help porting wolfSSL to your project, running into build failures, or want a port that is not yet in this repo, email support@wolfssl.com.

## How Patches Work

Each project directory is self-contained. There is no top-level build system — ports do not share a common configure or Makefile.

Within each directory you will find one of two layouts:

- **Patch files** (`.patch`): Apply against a fresh checkout of the specified upstream version using `git apply` or `patch -p1`. Follow the per-project `README` for exact version and apply order.
- **Modified source tree**: A copy of the upstream source with wolfSSL changes already applied. Build by following the per-project `README`.

General workflow:

```bash
# Example for a patch-based port
git clone <upstream-repo> && cd <upstream>
git checkout <version-tag>
patch -p1 < /path/to/osp/<project>/<project>.patch
# Follow the per-project README for configure flags and build steps
```

wolfSSL itself must be built and installed (or its source tree pointed to) before building the ported project. A typical wolfSSL build for porting work:

```bash
./configure --enable-opensslextra --enable-opensslall
make
sudo make install
```

Consult the per-project `README` for the exact wolfSSL configure flags that project requires.

## Ported Projects

Key projects with patches or build instructions in this repo:

| Directory | Upstream Project |
|-----------|-----------------|
| `openssh` / `openssh-patches` | OpenSSH — SSH client/server |
| `haproxy` | HAProxy — TCP/HTTP load balancer |
| `stunnel` | stunnel — TLS proxy wrapper |
| `lighttpd` | lighttpd — lightweight web server |
| `curl` (see `libssh2`) | cURL — URL transfer library |
| `nginx` | nginx — web server and reverse proxy |
| `mariadb` | MariaDB — MySQL-compatible database |
| `mosquitto` | Eclipse Mosquitto — MQTT broker |
| `openldap` | OpenLDAP — LDAP directory server |
| `grpc` | gRPC — RPC framework |
| `socat` | socat — multipurpose relay tool |
| `qt` | Qt — cross-platform application framework |
| `libssh2` | libssh2 — SSH2 client library |
| `net-snmp` | Net-SNMP — SNMP agent and tools |
| `krb5` | MIT Kerberos (krb5) — authentication protocol |

Additional ports are present in the repository — the table above covers the most commonly requested ones.

## Contributing

Contributions are welcome via the standard fork-and-PR workflow on GitHub.

- **Contributor agreement required.** External contributors must sign a contributor agreement before patches can be merged. Email support@wolfssl.com referencing your pull request.
- **Fork workflow.** Do not push branches directly to this repository. Fork to your personal GitHub account and open PRs from your fork.
- **Per-project scope.** Keep changes scoped to the port you are modifying. Do not reformat unrelated files.
- All CI checks must pass before merge.
