# DoN Range IModule (new, separate)

`don-range-imodule.tar` is a **new, separate** IModule generated from the
[don-range](https://github.com/spencer-dollahite/don-range) lab-family generator.
It does **not** replace `imodule.tar`; the existing labs are untouched.

It contains two labs from the fictional **NAVSTA Cutlass Bay** enclave:

| Lab | Runs on | What it exercises |
|-----|---------|-------------------|
| `don-recon-101` | stock bases only (build locally) | SMB/service recon from a user workstation |
| `don-ids-201` | custom bases `don.sensor`, `don.redteam` | Zeek/Snort detection of a cross-VLAN scan |

## How this differs from the current imodule

| | Current `imodule.tar` | New `don-range-imodule.tar` |
|---|---|---|
| Labs | `cs3670-syslog`, `file-system-permissions` | `don-recon-101`, `don-ids-201` |
| Authoring | hand-built per lab | generated from one world model (`world.yml`) |
| Contents | run-only (config/instr_config/docs) | **full** dirs incl. dockerfiles + container files (so you can `rebuild` locally to test) |
| Manuals | docx / html / pdf | **Markdown source → PDF + HTML** (pandoc, one shared theme) |
| Reports | docx template | **Markdown**, edited in vim, `submit` → single self-contained PDF to `mystuff` for LMS |
| Networking | single subnet | function-based VLANs, gateway routing + NAT, realistic inward DNS |
| Monitoring | n/a | passive tap → Zeek/Snort sensor over captured pcaps |
| Extras | n/a | per-user KeePassXC vaults; vim/tmux/bash-completion/Firefox on every container |

## Test it

The tar carries the full lab dirs, so you can build and run locally.

```bash
# 1. Load the imodule into your Labtainers install
imodule file:///absolute/path/to/don-range-imodule.tar
#    (or publish it and use the https URL)

# 2. Start with the simplest lab (stock bases; builds locally on first run)
labtainer don-recon-101
```

`don-recon-101` needs no custom images. If the framework tries to pull from the
`ssdollahite` registry and the image is not there yet, build it locally first:

```bash
cd $LABTAINER_DIR/scripts/labtainer-student/bin && ./rebuild don-recon-101
labtainer don-recon-101
```

`don-ids-201` additionally needs the custom base images built and available:

```bash
# from the don-range repo:
docker login -u ssdollahite            # run yourself; token stays local
cd bases && ./build_bases.sh don.sensor don.redteam    # add PUSH=1 to push
```

It also wants more RAM (sensor + gateway + hosts ~2.5 GB); check the generator's
dry-run budget line before running on an 8 GB VM.

## Notes

- Registry is `ssdollahite`. For normal student distribution (run-only imodule,
  images pulled from Docker Hub), push the lab and base images first, then a
  slimmer run-only tar can be produced. This tar is the **full** designer package
  for testing.
- To inspect without installing: `tar tf don-range-imodule.tar` and
  `tar xf don-range-imodule.tar -C /tmp/dr && ls /tmp/dr`.
