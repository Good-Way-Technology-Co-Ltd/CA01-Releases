# CA01 — Release Distribution

Official distribution point for **CA01** software updates, published by
**Good Way Technology Co., Ltd.**

> **This repository contains no source code.**
> It exists only to host signed update packages. Devices fetch and verify
> them automatically; you do not normally need to download anything here.

## Verifying a release

Every release carries `MANIFEST.json` (which lists the SHA-256 of every
other asset) and `MANIFEST.json.sig` (a detached signature over it).

Devices verify the signature before anything is unpacked. To check by hand:

```sh
echo 'ota@goodway namespaces="ota" <root public key>' > allowed_signers
ssh-keygen -Y verify -f allowed_signers -I ota@goodway -n ota \
           -s MANIFEST.json.sig < MANIFEST.json
```

Root key fingerprint — cross-check this against any copy you are given:

```
SHA256:Wyyzvu3bpazNdfysJJrwgDADB7qjdbmVrflQ6dNxLNo        (POC key — replaced before production)
```

## Asset names are stable

| file | what it is |
|------|------------|
| `box-update.tar.gz` | the appliance software package |
| `MANIFEST.json` | release metadata + SHA-256 of every asset |
| `MANIFEST.json.sig` | detached signature over the manifest |
| `worker-app-macos.dmg` | companion app (macOS) |
| `worker-app-windows.exe` | companion app (Windows) |
| `worker-app-linux.AppImage` | companion app (Linux) |

The newest release is always reachable at a fixed address, so devices never
need to call the GitHub API:

```
https://github.com/Good-Way-Technology-Co-Ltd/CA01-Releases/releases/latest/download/MANIFEST.json
```

## Releases are never deleted

Devices can roll back to **any** earlier version by re-fetching its package.

> **Deleting an old release breaks rollback for every device still on it.**
> Please do not remove past releases when tidying up.

## Licence

Proprietary — see [LICENSE](LICENSE). Third-party components included in the
packages are licensed under their own terms; see `THIRD-PARTY-NOTICES.md`
inside each package.

## Support

This repository is distribution only; issues here are not monitored.
