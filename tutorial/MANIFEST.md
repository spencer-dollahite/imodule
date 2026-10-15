# MANIFEST — DoN Range Zero-to-Lab tutorial figures

Every figure in the tutorial, with its provenance. Three kinds:

- **REAL (fresh)** — captured live for this tutorial on the DoN Range dev box, from the real stack
  (Xvfb `:99` @ 1920×1080×24, i3 with donlab's own config, Adwaita-dark, dark xterm, snap Firefox with
  donlab's manual profile; grabbed with `DISPLAY=:99 import -window root`). The lab ran under the real
  `donlab cs3670-lab1`; the manual/FRMS/bridge/tmux are the real services.
- **REUSED** — a real screenshot of the VirtualBox/UTM import wizard (identical across host OSes),
  taken from the published imodule student README (`imodule/docs/img`). Not freshly shot here.
- **PLACEHOLDER — NEEDS-A-SEAT** — cannot exist on this headless x86 build box (no Windows+VirtualBox,
  no Mac+UTM, no access to the course LMS). The figure is a labeled placeholder carrying the exact
  capture steps; it must be shot on a real seat before publishing.

Secrets policy: the course key, lab passwords and the CAC PIN that appear in the UI are **fictional
training values**; they are **redacted** in every delivered figure (black box, red label). No real
secret is shown anywhere. The shell prompt was set to `student@labtainer` so the build box's real
hostname does not leak; `127.0.0.1` lab URLs are shown as-is (not sensitive).

## Setup A — Windows 11 / x86 (per-platform preamble)
| Fig | File | Status | Notes / capture instruction |
|---|---|---|---|
| A1 | `setupA-01-vbox-install.png` | **PLACEHOLDER — NEEDS-A-SEAT** | Dark instruction card: install VirtualBox (Windows/Linux/Intel-Mac; no account) or VMware (free, Broadcom account). Shoot the installer + empty Manager on a real seat. |
| A1b | `setupA-01b-download.png` | **REAL** | Live dark-rendered capture of the official NPS Labtainers downloads page (nps.edu), VirtualBox `.ova` + VMware `.ova` highlighted. Captured via Xvfb + Firefox with a dark userContent.css. |
| A2 | `setupA-02-vbox-file-menu.png` | REUSED | VirtualBox *File ▸ Import Appliance* (imodule README). |
| A3 | `setupA-03-vbox-import-source.png` | REUSED | Import wizard: Source = Local File System. |
| A4 | `setupA-04-vbox-import-file.png` | REUSED | Import wizard: choose the `.ova`. |
| A5 | `setupA-05-vbox-import-settings.png` | REUSED | Import wizard: RAM/CPU review. |
| A6 | `setupA-06-vbox-import-progress.png` | REUSED | Import progress. |
| A7 | `setup-first-boot.png` | REUSED | First-boot desktop (guest). The *Windows-host framing* (VM window on a Windows 11 desktop) still **NEEDS-A-WINDOWS-SEAT**. |

## Setup B — Apple-Silicon Mac / arm64 (per-platform preamble)
| Fig | File | Status | Notes / capture instruction |
|---|---|---|---|
| B1 | `setupB-01-utm-install.png` | **PLACEHOLDER — NEEDS-A-MAC-SEAT** | Dark instruction card: install UTM (no account; VMware Fusion is a free, Broadcom-account alternative). Shoot on a Mac. |
| B1b | `setupB-01b-download.png` | **PLACEHOLDER — NEEDS-A-SEAT** | Dark instruction card. The OneDrive/SharePoint folder loaded anonymously (real file list: arm64 `.ova`, `.qcow2`, `.utm.zip`) but rendered **bright-white** and would not dark-render cleanly (SPA overrode the dark CSS), so per the no-bright-white rule it fell back to the card (accurate: `.ova` for VirtualBox/Fusion, `.utm.zip` for UTM). Re-shoot with SharePoint's native dark mode (needs sign-in). |
| B2 | `setupB-02-utm-welcome.png` | REUSED | UTM welcome (imodule README; home path masked in original). |
| B3 | `setupB-03-utm-open.png` | REUSED | UTM: Open the appliance. |
| B4 | `setupB-04-utm-library.png` | REUSED | UTM library with the appliance. |
| B5 | `setup-first-boot.png` | REUSED | Same first-boot frame as A7. arm64 appliance is lightdm/XFCE; *on-Mac framing* **NEEDS-A-MAC-SEAT**. |
| — | (VMware variant) | **MISSING** | `vmware-import.png` is referenced by the README but was never captured; **NEEDS-A-SEAT** if a VMware path is wanted. |

## Core — shared, every platform (all REAL / fresh)
| Fig | File | Status | What / how captured |
|---|---|---|---|
| 1 | `core-01-key.png` | **REAL** | `donlab --key cs3670:XXXX-XXXX-XXXX` + `donlab --version`, dark xterm, key redacted (full one-liner shown). |
| 2 | `core-02-doctor.png` | **REAL** | `donlab --doctor` under `DISPLAY=:99` (PASS for i3/X/clipboard). |
| 3 | `core-03-help.png` | **REAL** | `donlab --help`. |
| 4 | `core-04-start.png` | **REAL** | donlab's real start output for `cs3670-lab1` (rendered from the live run log — donlab hands the terminal to tmux on a fast returning-start, so the text frame is reconstructed from its actual stdout, `/tmp/don-tut/lab1-live.log`; see SANITY-LOG). |
| 5 | `core-05-desktop.png` | **REAL** | Live i3 desktop: tmux terminal (hi-issm01) + manual Firefox, placed by donlab's own i3 layout marks. CAC PIN redacted. |
| 6 | `core-06-i3-tiled.png` | **REAL** | i3: terminal + FRMS dashboard tiled on workspace 2. |
| 7 | `core-07-i3-fullscreen.png` | **REAL** | `i3-msg fullscreen enable` on FRMS (= Super+f). |
| 8 | `core-08-i3-restored.png` | **REAL** | fullscreen disable (= Super+f again). |
| 9 | `core-09-i3-ws-moved.png` | **REAL** | `move container to workspace 3` (= Super+Shift+3); ws bar shows 1 2 3. |
| 10 | `core-10-i3-ws-view.png` | **REAL** | `workspace number 3` (= Super+3); FRMS alone. |
| 11 | `core-11-tmux-base.png` | **REAL** | tmux session `lab-cs3670-lab1`, shell in hi-issm01 (content + status bar, composited). |
| 12 | `core-12-tmux-panes.png` | **REAL** | `Ctrl-b %` split (sent via xdotool) → two panes in the same host. |
| 13 | `core-13-tmux-copymode.png` | **REAL** | `Ctrl-b [` copy-mode + `?root` vi search. |
| 14 | `core-14-tmux-multihost.png` | REUSED | Multi-host tmux (imodule README); lab1 has one interactive host. |
| 15 | `core-15-manual.png` | **REAL** | Manual fullscreen in snap Firefox (donlab manual profile). CAC PIN redacted. |
| 16 | `core-16-task.png` | **REAL** | Task 1 (command boxes + writebox), reached via TOC click. |
| 17 | `core-17-writebox-checkwork.png` | **REAL** | Answer typed into the live writebox; inline "Looks right"; progress → 1/30. |
| 18 | `core-18-glossary.png` | **REAL** | Live hover on "confidentiality" → glossary popover. |
| 19 | `core-19-bearings.png` | **REAL** | Bearings modal (Credentials tab). Passwords + CAC PIN redacted. |
| 20 | `core-20-actions.png` | **REAL** | Actions menu (checkwork / stoplab / Reset). |
| 21 | `core-21-finish-modal.png` | **REAL** | "Finish & build your Lab Report" modal (Download Lab Report). |
| 22 | `core-22-report-answers.png` | **REAL** | Downloaded Lab Report (draft path), answers section. |
| 23 | `core-23-report-standing.png` | **REAL** | Same report, FRMS + Standing & CTF + Progress sections. |
| 24 | `core-24-labfile.png` | **REAL** | `ls -lh ~/labtainer_xfer/cs3670-lab1/*.lab` — the real `.lab` artifact. |
| 25 | `core-25-lms-upload.png` | **PLACEHOLDER — NEEDS-A-SEAT (external LMS)** | Shoot on the real course LMS: assignment page, file picker on the `.lab`, submitted confirmation. |

## Summary
- **REAL (fresh capture):** 23 figures (Core 1–13, 15–24).
- **REUSED (real, from README):** 10 figures (Setup A2–A7, B2–B5, Core 14 — note A7/B5 share one file).
- **PLACEHOLDER — NEEDS-A-SEAT:** 3 figures (A1 Windows install, B1 Mac install, 25 LMS) + the
  Windows/Mac *host-framing* of the first-boot frame, + the optional VMware variant.

## Raw, un-annotated captures
Kept under `images/raw/` (e.g. `03a_key.png`, `04b_desktop.png`, `06a_tmux_base.png`, …) so figures can
be re-cropped/re-annotated without re-running the lab. Reused source assets are under `images/setup/`.

---

## Dark-theme audit & re-capture pass (owner hard requirement: zero bright-white UI)
Every PNG under `images/` was audited for near-white pixels. Offenders found and FIXED:
- **Lab Report** (`core-22`, `core-23`) — was a bright-white print document. The product's report export
  is now **genuinely dark** (commit 482d516: dark `#12232e` + light text in all cases incl. Save-as-PDF
  via `print-color-adjust`; browser print header/footer dropped via `@page{margin:0}`). The manual was
  **re-rendered from current source** (`gen_lab.py` → pandoc, revision v0.0.020) and a **real report built
  fresh** and screenshotted — no CSS-injection hack. Confirmed 0% bright-white.
- **Terminal shots** (`core-05` desktop, `core-11`/`12`/`13` tmux) — donlab had opened a default
  **white** xterm. **Re-captured** with a dark xterm (`#1b1b1b`) attached to the real tmux session.
- **Firefox chrome** — forced `firefox-compact-dark` on the manual profile; the URL bar / tab strip are
  dark in every chrome-visible shot (`core-05`).
Re-audit result: **no image exceeds ~0.5% near-white** (the 0.5% is the VirtualBox progress dialog, a
medium-grey reused asset — not bright white). Zero bright-white UI remains.

**Setup placeholders — dark-mode capture requirement (for whoever shoots them on a real seat):** capture
with the **host OS in dark mode** — Windows 11 dark theme + dark VirtualBox chrome (A1), macOS dark +
dark UTM chrome (B1), and a dark LMS theme (25). The reused VirtualBox/UTM wizard dialogs are medium-grey
(Qt dialogs); re-shoot them in dark mode on the real seat if a fully-dark setup half is wanted.

## Animated clips (`clips/`)
Short, per-action clips for inline autoplay in a GitHub README (`![](clips/<name>.webp)`): an animated
**WebP** (primary, small, full-colour) + a **GIF** fallback. Built with ffmpeg from the annotated frames
(960 px wide, 12–15 fps, 2–4 s, stepped where only discrete states exist). All are **dark**.

| Clip | Action | Source frames | Status |
|---|---|---|---|
| `doctor` | donlab --doctor → ready | core-02 | REAL |
| `start` | donlab cs3670-lab1 | core-04 | REAL (stdout-rendered start text) |
| `desktop` | the lab desktop | core-05 | REAL (dark) |
| `i3-fullscreen` | Super+f fullscreen & back | core-06→07→08 | REAL |
| `i3-workspace` | Super+Shift+3 then Super+3 | core-06→09→10 | REAL |
| `tmux-panes` | Ctrl-b % split | core-11→12 | REAL (dark) |
| `tmux-copymode` | Ctrl-b [ vi copy-mode | core-12→13 | REAL (dark) |
| `writebox` | write (autosave) + self-check locks | core-16→17 | REAL |
| `glossary` | hover popover | core-18 | REAL |
| `bearings` | briefing card | core-19 | REAL (creds redacted) |
| `export` | Finish & build report | core-21→22→23 | REAL (dark report) |
| `labfile` | the .lab on disk | core-24 | REAL |
| `key` | enroll one-liner | core-01 | REAL (key redacted) |
| `manual` | the manual | core-15 | REAL |
| `setupA-import` | VirtualBox import → first boot | setupA-02..06 + first-boot | REUSED assets |
| `setupB-import` | UTM open → first boot | setupB-02..04 + first-boot | REUSED assets |

Long-form (for the local `vid.html`, which can play anything):
- `vid-core.mp4` (~1.8 MB, 25 segments) — the whole Core, narrated (STORYBOARD narration burned as a
  lower-third bar). Also `vid-core.webp` (~0.4 MB) as a long autoplay WebP.
- `vid-setupA.mp4`, `vid-setupB.mp4` — the two narrated setup preambles (include the A1/B1 placeholders).

**Long-form method chosen: narrated slideshow** from the existing annotated frames + STORYBOARD
narration — NOT a fresh ffmpeg `x11grab` screencast. Rationale: the capture environment was already torn
down and a full re-run of the lab for smooth-motion video was out of scope for this focused clip pass.
A real screencast remains a future option (restart the lab on Xvfb, drive the Core actions, `x11grab`).

`vid.html` is the local player (platform picker → setup mp4 + Core mp4 + the short-clip grid).
`index.html` is the stills gallery. Both are dark-themed.

## No blank gaps (owner requirement)
Every step has a dark figure. The three steps that cannot be captured on this build box —
**A1** (VirtualBox install, Windows), **B1** (UTM install, Mac), **25** (LMS upload) — are rendered as
**dark instruction cards** (`#12232e`, legible, same landscape framing) that carry the student's steps
for that step, plus a footer tag that they are placeholders pending a real-seat capture. They remain
PLACEHOLDER in the table above. When shot for real, capture with the **host OS in dark mode**.

## Final audit (settled)
- **Zero bright-white UI:** images max 0.4%, animated WebP max 0.3%, GIF max 0.3%, MP4 max 0.2% near-white.
- **Secrets:** only the course key is shown redacted (`cs3670:XXXX-XXXX` / `<your-key>`) in the full
  one-liner; the CAC PIN and lab passwords are redacted wherever they appear (figures 5, 15, 19). No
  real key/token/PIN/private URL anywhere; text deliverables use `<your-key>` / `<your-email>`.
- **Clarity/cropping pass:** terminal shots cropped tight to content (bigger, no empty expanse); the
  Lab Report cropped to its content column; tmux composited to content + status bar; callouts are
  high-contrast and do not cover key content; window size/theme/aspect consistent across the Core set.


## Consolidated fix pass (owner-approved) — figures/clips changed
- **Re-annotated** (caption/content corrected to match the fixed prose, no re-capture needed):
  `core-01` (enroll: `<your-key>` token tied to the redaction, full key-install reply quoted),
  `core-17` (the three controls shown correctly: writebox autosaves / "Check my answer" locks on first
  click / progress bar advances on "Mark complete"), `core-19` (dropped "/SIEM"; "a SIEM appears in
  later labs"), `setup-first-boot` (login-then-desktop wording; wrong "import wizard" provenance removed).
- **New dark instruction cards:** `setupA-01b-download.png`, `setupB-01b-download.png` (OneDrive
  download + the Mac `.utm.zip` unzip step).
- **Rebuilt clips** whose frames changed: `key`, `writebox`, `bearings`, `setupA-import`,
  `setupB-import` (download card prepended), and the long-form `vid-core.mp4` / `vid-setupA.mp4` /
  `vid-setupB.mp4` (download/unzip segments added).
- **VMware** is a supported hypervisor (free, needs a Broadcom account). No VMware import screenshot
  exists yet — **NEEDS-A-SEAT** if a VMware-specific figure is wanted; the text notes the OVA imports
  the same way as VirtualBox.
- Intel Mac is treated as **native x86-64** (Setup A); all "emulation/slow" wording for Intel Mac was
  removed across the text, pages, and storyboard.


## Final spec + source + hypervisor pass (owner-confirmed)
- **Spec table** (TUTORIAL top + index.html) is Minimum vs Recommended: Host OS 64-bit Win 10/11 /
  macOS / Linux; Host RAM 16 GB (VM uses 8 GB) / 16 GB+; Guest RAM 8 GB / 8 GB+; Guest vCPU 2 / 4+;
  free host disk ~80 GB / ~120 GB+ (60 GB guest disk + ~5 GB download + headroom). "+" = this or more
  without starving the host. CPU virtualization (VT-x/AMD-V) only on x86 hosts; Apple Silicon needs none.
- **Download sources corrected:** x86_64 appliance = the **NPS downloads page** (A1b, now a REAL dark
  capture); arm64 appliance = the **OneDrive folder** (B1b card: `.ova` for VirtualBox/Fusion,
  `.utm.zip` for UTM).
- **Hypervisor matrix:** x86 hosts (Windows/Linux/Intel-Mac) = VirtualBox or VMware; Apple Silicon =
  VirtualBox (preferred) / VMware Fusion / UTM, all native arm64. Emulation (x86 on Apple Silicon)
  stays the slow last resort. Intel Mac is native x86 (Setup A); no "emulation/slow" wording for it.
- **Re-annotated/rebuilt this pass:** `core-01`, `core-17` (three controls), `core-19`, `setup-first-boot`;
  new/real cards `setupA-01` `setupA-01b`(REAL) `setupB-01` `setupB-01b`(card) `core-25`; rebuilt clips
  `key` `writebox` `bearings` `setupA-import` `setupB-import` and long-form `vid-core.mp4`
  (C17 narration corrected) / `vid-setupA.mp4` (NPS) / `vid-setupB.mp4` (OneDrive both files).
