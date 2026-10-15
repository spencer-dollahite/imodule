# DoN Range — Zero-to-Lab: Video Storyboard & Script

A branching onboarding video. The viewer picks a platform on the landing page; the player shows the
matching **Setup preamble**, then the **shared Core**. Capture the Core **once** and reuse it in both
cuts (Windows and Mac). Target length: Setup ~2 min each, Core ~7–9 min, total ~9–11 min per platform.

Format per shot: **[SHOT] source image · on-screen action · NARRATION.** Narration is in the
house instructor voice (formal, terse). Keep callouts/zooms on the boxed regions in each figure.

---

## COLD OPEN (shared, ~15 s)
- **[TITLE]** DoN Range wordmark on black → the dark i3 desktop (`core-05-desktop.png`) fades in.
- NARRATION: "This is DoN Range. By the end of this video you will have installed the lab environment,
  started your first lab, and submitted it. Pick your computer on the screen; the second half is the same for everyone. Have ready: your
  instructor's OneDrive link, your VM login, and your cs3670 key."

---

## SETUP A — Windows 11 / x86  (branch A)

- **[A1]** `setupA-01-vbox-install.png` — *(record on a Windows 11 seat: download page → installer →
  VirtualBox Manager).* NARRATION: "On a Windows, Linux, or Intel-Mac machine, install VirtualBox from virtualbox.org (no
  account). VMware is a free alternative. Accept the defaults, then open VirtualBox Manager."
- **[A1b]** `setupA-01b-download.png` — NARRATION: "On the official NPS downloads page, download the
  x86_64 appliance O-V-A for your hypervisor. VirtualBox and VMware both use the O-V-A. Several gigabytes;
  don't cancel. It imports directly, no unzip."
- **[A2]** `setupA-02-vbox-file-menu.png` — highlight File ▸ Import Appliance. NARRATION: "In VirtualBox,
  or VMware, choose File, Import Appliance."
- **[A3]** `setupA-03-vbox-import-source.png` — NARRATION: "Leave the source on Local File System."
- **[A4]** `setupA-04-vbox-import-file.png` — point at the folder icon. NARRATION: "Pick the appliance
  dot-O-V-A you downloaded."
- **[A5]** `setupA-05-vbox-import-settings.png` — NARRATION: "Give it as much memory and CPU as you can
  spare — eight gigabytes or more — and import."
- **[A6]** `setupA-06-vbox-import-progress.png` — NARRATION: "The import runs once. When it finishes,
  start the VM."
- **[A7]** `setup-first-boot.png` — NARRATION: "It boots to the desktop. Log in with your student
  account. From here, every platform is the same." → cut to CORE.

## SETUP B — Apple-Silicon Mac / arm64  (branch B)

- **[B1]** `setupB-01-utm-install.png` — *(record on a Mac seat: UTM install, appliance download).*
  NARRATION: "Apple Silicon runs the arm64 appliance natively on three hypervisors: VirtualBox is
  recommended, or VMware Fusion, or UTM. Install one. (An Intel Mac is x86 — follow Setup A.)"
- **[B1b]** `setupB-01b-download.png` — NARRATION: "The OneDrive folder has the arm64 O-V-A and a
  dot-U-T-M-dot-zip. VirtualBox or Fusion use the O-V-A (imports directly); UTM uses the dot-U-T-M-dot-zip
  (double-click to extract the bundle)."
- **[B2]** `setupB-02-utm-welcome.png` — NARRATION: "Open UTM."
- **[B3]** `setupB-03-utm-open.png` — NARRATION: "Use Open, and point it at the appliance you
  downloaded."
- **[B4]** `setupB-04-utm-library.png` — NARRATION: "It joins your library. Press start. If it has no
  internet, set the network mode to Emulated VLAN."
- **[B5]** `setup-first-boot.png` — NARRATION: "It boots to the desktop. Log in. From here, every
  platform is the same." → cut to CORE.

---

## CORE (shared — capture once, reuse in both cuts)

- **[C1]** `core-01-key.png` — type the one-liner, key field blurred. NARRATION: "Open a terminal.
  Enroll once with donlab dash-dash-key, your course, colon, your key. You paste your own key where the
  Xs are; keep it private."
- **[C2]** `core-02-doctor.png` — scroll the PASS list. NARRATION: "Run donlab dash-dash-doctor. Green
  means the VM is ready — Docker, the display, the i3 session, the clipboard, the registry. Yellow is
  just advice."
- **[C3]** `core-03-help.png` — NARRATION: "donlab dash-dash-help is your map: enroll, start a lab,
  check the VM, reset a lab, free disk. Your submitted reports are never touched."
- **[C4]** `core-04-start.png` — NARRATION: "Start the lab: donlab cs3670-lab1. The first run pulls the
  images and takes a few minutes; after that it is quick. It prints the manual link and lays your hosts
  out in tmux." *(x86 pulls x86-64 images, Apple Silicon pulls arm64 — you type nothing different.)*
- **[C5]** `core-05-desktop.png` — pan left→right across the two tiles. NARRATION: "You land in the i3
  desktop. Your terminal is on the left, logged into the lab host. The manual is on the right. Read the
  scenario brief, then work the tasks top to bottom."
- **[C6]** `core-06-i3-tiled.png` — NARRATION: "i3 tiles windows — no overlap, no hunting. Super is the
  Windows or Command key. Super and arrows move focus."
- **[C7]** `core-07-i3-fullscreen.png` — press-key overlay. NARRATION: "Super-f takes the focused window
  fullscreen — handy for reading a dashboard."
- **[C8]** `core-08-i3-restored.png` — NARRATION: "Super-f again puts it back."
- **[C9]** `core-09-i3-ws-moved.png` — NARRATION: "Super-shift-three sends a window to workspace three.
  The current desktop is left with just the terminal."
- **[C10]** `core-10-i3-ws-view.png` — NARRATION: "Super-three follows it there; Super-one brings you
  back. Workspaces are virtual desktops — keep the manual on one, your work on another."
- **[C11]** `core-11-tmux-base.png` — zoom the status bar. NARRATION: "Your terminals live in tmux. The
  prefix is Control-b. This shell is inside the lab host; the blue bar names it. Control-b, d detaches —
  the lab keeps running."
- **[C12]** `core-12-tmux-panes.png` — NARRATION: "Control-b, percent splits side by side; Control-b,
  quote splits top and bottom. Each pane is another shell in the same host."
- **[C13]** `core-13-tmux-copymode.png` — NARRATION: "Control-b, open-bracket scrolls back in copy-mode.
  It is vi-keyed — h-j-k-l to move, slash to search. The editor everywhere is vim."
- **[C14]** `core-14-tmux-multihost.png` — NARRATION: "In labs with several hosts, each host is its own
  tmux window. Control-b, w lists them; Control-b and a number jumps straight there."
- **[C15]** `core-15-manual.png` — NARRATION: "The manual: a contents list on the left, and up top,
  Bearings, Actions, and Download Lab Report."
- **[C16]** `core-16-task.png` — NARRATION: "A task mixes reading, command boxes you run in your
  terminal, and writeboxes for your answers."
- **[C17]** `core-17-writebox-checkwork.png` — type into the box. NARRATION: "Three separate things:
  write your answer and it autosaves; Check my answer gives feedback and locks that answer; ticking Mark
  complete advances the progress bar." 
- **[C18]** `core-18-glossary.png` — hover the term. NARRATION: "Hover a dotted term for its definition —
  our definition first, with the authoritative source."
- **[C19]** `core-19-bearings.png` — NARRATION: "Bearings is your briefing card — who you are on each
  host, and the CAC PIN for FRMS. These are training values. In this lab, FRMS runs inside the enclave;
  you open it from the workstation's Firefox and sign in with your CAC."
- **[C20]** `core-20-actions.png` — NARRATION: "Actions drives the live lab — re-check your work, stop
  the lab, or reset it."
- **[C21]** `core-21-finish-modal.png` — NARRATION: "When you finish, Download Lab Report, then Finish
  and build report: it checks your work, stops the lab, packages your submission, and builds the
  report."
- **[C22]** `core-22-report-answers.png` — NARRATION: "The report gathers every answer under its prompt.
  It is a clean, printable document — print it or save a PDF."
- **[C23]** `core-23-report-standing.png` — NARRATION: "Further down: what you did in FRMS, your
  standing and the CTF flags you found, and your progress and time in the lab."
- **[C24]** `core-24-labfile.png` — NARRATION: "Your submission is the dot-lab file in labtainer-xfer."
- **[C25]** `core-25-lms-upload.png` — *(record on the real LMS.)* NARRATION: "Upload that dot-lab file
  to the assignment in your course LMS, and submit. That's the whole loop — install, boot, start, work,
  finish, submit."

---

## CLOSE (shared, ~8 s)
- **[OUTRO]** back to the dark desktop. NARRATION: "Everything after the desktop is identical on Windows
  and Mac. Good hunting."

### Production notes
- Keep window size and the dark theme constant across Core shots (they already are: 1920×1080, i3,
  Adwaita-dark, dark Firefox/xterm).
- For live-action re-shoots of Core, drive the same path: `donlab --key`, `--doctor`,
  `donlab cs3670-lab1`, then the i3 / tmux / manual actions in the order above.
- Setup A1/B1 and C25 (LMS) **must** be shot on a real Windows seat, a real Mac, and the real LMS —
  they cannot be produced on the headless build box.
