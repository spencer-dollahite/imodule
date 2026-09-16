# DoN Range imodule (encrypted, per course)

This repository is the distribution point for the DoN Range Labtainers labs and the `donlab`
launcher, for CS3600, CS3670 and CS3690. Students do not clone it; the launcher fetches what
it needs from here at every lab start. Student setup is in [README.md](README.md).

## What is published here

| File | What |
|------|------|
| `imodule-cs3600.tar.enc` (+ `.sha256`) | the CS3600 labs, AES-256 encrypted under the CS3600 key |
| `imodule-cs3670.tar.enc` (+ `.sha256`) | the CS3670 labs, AES-256 encrypted under the CS3670 key |
| `imodule-cs3690.tar.enc` (+ `.sha256`) | the CS3690 labs, AES-256 encrypted under the CS3690 key |
| `donlab` (+ `.sha256`) | the launcher, keyless (holds no course key); the copy the launcher self-updates from |

Each course has its own encrypted bundle and its own key. The container images are pulled
from the public registry, so the bundle is what makes a course's labs installable and
gradeable: without the course key, the launcher cannot decrypt that course's labs.

## Students

Use the `donlab` launcher (this repository's copy, or the one on your VM appliance). Install
the key your instructor gives you for your course, once, then start a lab; the launcher picks
the bundle and key for the course from the lab id:

```bash
donlab --key cs3670:<key>     # once per course you are enrolled in
donlab cs3670-lab1
```

`imodule` never sees ciphertext; `donlab` decrypts your course's bundle to a local file and
hands that to `imodule`. See [README.md](README.md) for full setup and troubleshooting.

## Publishing (instructor)

From the generator repository (`spencer-dollahite/don-range`): `dist/don-pack` builds one
`imodule-<course>.tar.enc` per course from the per-course keys, `dist/publish-donlab` writes
the keyless launcher, and `dist/publish-imodule` pushes both to this repository. Students pick
up the change on their next `donlab`.
