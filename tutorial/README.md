# DoN Range — Zero-to-Lab onboarding tutorial (GitHub issue #92)

A screenshot walkthrough + video storyboard that takes a brand-new student from nothing to running
and submitting their first lab (CS3670 Lab 1).

## Contents
- **`index.html`** — landing page: pick your platform (Windows/x86 or Mac/arm64), then it shows your
  setup preamble followed by the shared Core. Open it in a browser.
- **`TUTORIAL.md`** — the full written walkthrough (Setup A, Setup B, shared Core, LMS).
- **`STORYBOARD.md`** — branching video shot list + narration script.
- **`MANIFEST.md`** — every figure: REAL (freshly captured here) vs REUSED vs PLACEHOLDER
  (NEEDS-A-SEAT), with how each was captured.
- **`SANITY-LOG.md`** — exactly what was run and verified end-to-end, and what diverged.
- **`images/`** — annotated figures (`core-*`, `setupA-*`, `setupB-*`, `setup-first-boot`,
  `core-25-lms-upload`). `images/raw/` keeps the un-annotated grabs; `images/setup/` keeps the
  reused source assets.

## Structure
Per-platform **setup preambles** (A: Windows/Linux/**Intel-Mac** x86-64 → VirtualBox or VMware → the
official NPS x86_64 appliance; B: Apple-Silicon Mac → UTM → arm64 appliance) + ONE shared **Core** (donlab, i3, tmux, manual/features, Lab Report
export, LMS upload). The Core is identical on every platform; only the container-image architecture
(x86-64 vs arm64) differs underneath.

## Prerequisites a student needs (stated at the top of the tutorial)
The instructor's OneDrive appliance link, the VM login, the cs3670 course key; a 64-bit host with CPU
virtualization enabled, 8 GB+ RAM, ~30 GB free disk. Native-first hypervisor choice; emulation only as
a slow last resort.

## Before publishing
Shoot the 3 NEEDS-A-SEAT placeholders (VirtualBox install on Windows 11; UTM install on a Mac; the
real LMS upload). See MANIFEST.md / SANITY-LOG.md. Do not push to the imodule repo until owner review.
