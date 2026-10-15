# SANITY LOG — what was actually run and verified

Build host: headless **x86-64 AWS dev box** (2 vCPU, 8 GB), no display hardware. All GUI work ran on a
virtual X server. This box **cannot** run VirtualBox-on-Windows or UTM-on-macOS, so Setup steps 1–2
were not executed here (see MANIFEST placeholders).

## Capture environment (verified working)
- `Xvfb :99 -screen 0 1920x1080x24` — virtual display.
- `i3` 4.23 started on `:99` with a **faithful copy of donlab's own i3 config** (extracted from
  `dist/donlab` `i3_config_text`: same `$mod`, splits, workspaces, `Super+f`, dark `bar`/i3status).
- Dark everywhere: `~/.config/gtk-3.0/settings.ini` prefer-dark; dark xterm (`#1b1b1b`/`#e6e6e6`);
  snap Firefox on donlab's manual profile (`~/snap/firefox/common/don-range-manual`, Adwaita-dark).
- Grabs: `DISPLAY=:99 import -window root`. UI driven with `i3-msg` and `xdotool`.
- The **headless smoke overrides were NOT used** (`DONLAB_NO_DARK` / `NO_I3` / `NO_LAYOUT` all unset) —
  this is the real student i3 + dark experience.

## donlab (verified)
- Used `dist/donlab` (the repo's **keyless** master — per-course keys are injected only at publish).
- To exercise the real **returning-student** path offline: installed a **placeholder** key
  (`donlab --key cs3670:XXXX…`) and pre-seeded `~/.config/don-range/installed-cs3670.sha256` with the
  published bundle's sha, so donlab reported **"Lab bundle is already up to date"** and started from the
  locally installed lab defs + cached images (no network decrypt needed).
- Verified clean output: `donlab --version` (1.4.23, channel prod, x86_64), `donlab --help`,
  `donlab --doctor` (all green PASS under `:99` except advisory WARNs: 2-core CPU, snap-Firefox INFO).
- `ensure_i3_session` correctly detected the running i3 and **did not reboot** (it only wrote config
  files). `ensure_cgroup2` was a no-op (box is already cgroup v2). No reboot occurred.

## Lab run (verified end-to-end)
- `donlab cs3670-lab1` started the real lab: **2 containers up** (`cs3670-lab1.hi-issm01.student`,
  `…hi-web01.student`), "2 completed initialization. Done."
- Manual **bridge** `127.0.0.1:5173` → `/api/ping` = `{"ok": true, "bridge": "don-range"}`.
- **FRMS** `127.0.0.1:5174` → `/api/ping` = `{"ok": true, "system": "FRMS"}`; dashboard rendered.
- tmux session `lab-cs3670-lab1` created (shell inside hi-issm01 as persona `dholloway`).
- Manual served at `http://127.0.0.1:5173/cs3670-lab1.html` and rendered dark in snap Firefox.

## Features exercised (verified, each captured)
- i3: `Super+f` fullscreen + restore; `Super+Shift+3` move + `Super+3` view (workspace bar 1→2→3).
- tmux: `Ctrl-b %` pane split (opened a second shell in the same host); `Ctrl-b [` vi copy-mode with
  `?` search prompt; status bar shows session/host.
- Manual: writebox autosave + Check Work ("Looks right", **progress advanced 0→1/30, task checked**);
  glossary hover popover ("confidentiality", owner + source); Bearings modal; Actions menu
  (checkwork/stoplab/reset); "Finish & build your Lab Report" modal.
- Export: "Just download a draft" produced **`report-cs3670-lab1-verify.html` (66.7 KB)** containing the
  typed answer, **What you did in FRMS**, **Standing & CTF** (Rank Plebe, CTF 0/8), **Progress & Check
  Work** — confirmed by reading the file's sections.
- `stoplab cs3670-lab1` produced the real submission artifact
  `~/labtainer_xfer/cs3670-lab1/<email>.cs3670-lab1.lab`.

## Things that failed / diverged (honest notes)
1. **snap Firefox cannot read a `/tmp` profile** (confinement → "Profile Missing"). Fixed by using
   donlab's own snap-safe profile dir under `~/snap/firefox/common` and serving pages over `http://127.0.0.1`
   (snap can't read `file://` under `/tmp` either). This matches the known donlab behaviour.
2. **Start-sequence frame (Fig 4):** on a fast returning-start, donlab `exec`s `tmux attach` and the
   terminal is replaced by the tmux view before the scrollback can be grabbed. Fig 4 therefore renders
   donlab's **real stdout** (captured to `/tmp/don-tut/lab1-live.log`) with the typed command prepended —
   faithful to the bytes donlab printed, not a fresh terminal grab. Flagged in the MANIFEST.
3. **FRMS in CS3670 Lab 1 is an in-lab (CAC) service** reached from inside the workstation container.
   The dashboard figures (6–10) use the **same FRMS app** served on the host port `:5174`; the authentic
   CAC-login-inside-the-workstation flow was **not** driven here (it needs the container's Firefox + the
   soft-CAC PKCS#11 flow). The UI shown is the real FRMS; the login path is described, not captured.
4. **Account identity in filenames/report:** this box's framework account is `verify@nps.edu`, so the
   `.lab` and report are named for it. A real student sees their own email; the tutorial text uses
   `<your-email>`.
5. **Lab Report theme:** SUPERSEDED — the product's report export is now **genuinely dark** (commit
   482d516: `#12232e` + light text in all cases incl. Save-as-PDF). The report figures were re-rendered
   from current source and re-shot dark; the earlier "light by design" note no longer applies.
6. **`pkill -f firefox` is unsafe here** (it matches the agent's own shell). Firefox was always killed
   by window PID (`xdotool getwindowpid`) or by the exact snap binary path. No stray processes killed.
7. **CPU=2** on the build box → doctor WARN "builds will be slow"; not a defect, expected on this host.

## Not done (by instruction)
- **Nothing was pushed** to the imodule GitHub repo (or anywhere). All artifacts are local under
  `dist/tutorial/`.
- The host was **not rebooted**; the owner's tmux client was **not** touched (captures used a dedicated
  tmux session on display `:99`, separate from any existing session).

## What's left before publishing
- Shoot the 3 real-seat placeholders: **A1** (VirtualBox install on Windows 11), **B1** (UTM install on
  an Apple-Silicon Mac), **25** (upload on the real course LMS); optionally the Windows/Mac *host
  framing* of the first-boot frame and a **VMware** variant.
- Optional: capture the authentic **in-workstation CAC login to FRMS** for Lab 1 (needs a real seat or
  the geckodriver-in-container recipe) if a CAC-login figure is wanted beyond the dashboard.
- Owner review of wording/figures, then publish to the imodule repo as a separate reviewed step.

## Dark-theme enforcement pass (owner hard requirement) + clips
- Audited every `images/*.png` for near-white. Offenders: the **Lab Report** (76–78%) and the
  **terminal/desktop** shots (40–70% — donlab had opened a *default white xterm*).
- **Terminal/desktop re-captured dark:** restarted Xvfb/i3 + the lab, attached a **dark xterm**
  (`#1b1b1b`) to the real `lab-cs3670-lab1` tmux session, re-shot `core-05/11/12/13`; forced
  `firefox-compact-dark` on the manual profile so the browser **chrome** is dark too.
- **Lab Report:** the product's export is now genuinely dark (HEAD = commit 482d516). I **re-rendered
  the manual from current source** (`generator/gen_lab.py labs/cs3670-lab1.yml --out $LT/labs --force`
  → `pandoc` build; revision v0.0.020), served it (donlab bridge on :5175 — :5173 was held by the
  preview server, left untouched), typed the Task-1 answer, and built a **real report** via Download
  Lab Report → draft. The downloaded report has `body{background:#12232e}` + `print-color-adjust` +
  `@page{margin:0}`. Re-shot `core-22/23` from the real dark report — no CSS hack.
- **Final audit (near-white, PASS ≤3%):** images max **0.4%**; animated WebP max **0.3%** (all valid,
  multi-frame, loop=0); GIF max **0.3%**; MP4 max **0.2%**. **Zero bright-white UI remains.**
- **Clips produced** with ffmpeg (libwebp_anim + gif + libx264): 16 short per-action clips
  (`clips/*.webp` + `.gif`, 11–112 KB webp / 29–293 KB gif, 2–4 s, dark) for README inline autoplay;
  long-form narrated `vid-core.mp4` (~1.8 MB) + `vid-setupA/B.mp4` + `vid-core.webp` for `vid.html`.
  Long-form = narrated slideshow from the annotated frames (chosen over a fresh x11grab screencast to
  keep this a bounded clip pass). `vid.html` is the local player; `index.html` the stills gallery.
- A stray port conflict was noted and respected: `127.0.0.1:5173` is the owner/coordinator's tutorial
  **preview server** (serving an older render); donlab's capture bridge ran on **:5175**. The preview
  server was NOT touched.
