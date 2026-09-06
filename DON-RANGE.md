# DoN Range imodule (encrypted)

This repo hosts two imodules side by side:

| File | What |
|------|------|
| `imodule.tar` | the original legacy imodule (unchanged) |
| `imodule.tar.enc` (+ `.sha256`) | the new DoN Range labs, **AES-256 encrypted** |

The encrypted bundle contains four labs in the new format, each with built
PDF/HTML manuals and report tooling:

| Lab | What it exercises |
|-----|-------------------|
| `don-recon-101` | SMB/service recon from a user workstation |
| `don-ids-201` | Zeek/Snort detection of a cross-VLAN scan |
| `file-system-permissions` | nginx path traversal, offline shadow cracking (rockyou), remediation |
| `cs3670-syslog` | rsyslog -> loghost -> Wazuh; triage fast/slow brute force vs a real login |

## Students

Use the `donlab` launcher from the generator repo
(`spencer-dollahite/don-range`, `dist/donlab`). It pulls this encrypted bundle,
decrypts it (key baked in), installs it via `imodule`, and starts the lab -- so
every start gets the latest:

```bash
donlab <labname>
```

`imodule` never sees ciphertext; `donlab` decrypts and hands it a local file.
Publishing an update is just `don-pack` + replacing `imodule.tar.enc` (+ `.sha256`)
here; students pick it up on their next `donlab`.
