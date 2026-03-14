# chan_sccp

`chan_sccp` is a maintained downstream fork of the Cisco Skinny/SCCP channel driver for Asterisk.

This repository is not intended to be a 1:1 mirror of upstream. It began from the upstream `chan-sccp/chan-sccp` codebase, but this line has been reworked to keep the driver useful on newer Asterisk releases, newer Linux distributions, and additional deployment targets where the older code no longer fit cleanly.

## What Is Different Here

This fork exists to carry practical compatibility and operational work, including:

- support for newer Asterisk versions beyond the range handled by the source we started from
- portability updates for newer Linux releases and related platform variants
- RTP and voice path fixes to restore working media streams
- additional maintenance and integration changes needed for real deployments

The goal of this tree is straightforward: keep SCCP endpoints usable on modern systems.

## Scope

This repository should be read as the maintained project for this fork, not as upstream documentation with a few local patches layered on top.

Upstream history matters for provenance, but the active focus here is:

- building against newer Asterisk branches
- keeping the module usable across newer distro environments
- preserving working call handling and media flow
- carrying deployment-driven fixes that may not exist upstream

## Build Overview

Typical build flow:

```bash
./configure
make -j"$(nproc)"
make install
make reload
```

If you change `configure.ac`, `Makefile.am`, or related autoconf inputs, regenerate build machinery with:

```bash
./tools/bootstrap.sh
```

## Requirements

Common requirements include:

- a supported Asterisk source/header installation for the target version
- standard build tooling such as `gcc` or `clang`, `make`, `sed`, `awk`, and `tr`
- XML/XSLT development libraries
- OpenSSL development libraries
- `gettext`

Exact package names vary by distribution.

## Asterisk Notes

Before loading `chan_sccp`, make sure the native Skinny channel driver is not competing for the same endpoints.

Required supporting Asterisk modules commonly include:

- `app_voicemail`
- `bridge_simple`
- `bridge_native_rtp`
- `bridge_softmix`
- `bridge_holding`
- `res_stasis`
- `res_stasis_device_state`

Actual module requirements can vary by Asterisk version and deployment profile.

## Documentation In Tree

This repository still carries useful historical material from the inherited codebase, including:

- `INSTALL`
- `doc/`
- `tools/`

Treat those files as technical reference material, not as a full statement of this fork's project identity.

## Provenance

This project stems from the upstream [`chan-sccp/chan-sccp`](https://github.com/chan-sccp/chan-sccp/) codebase.

This fork keeps the same GPL licensing already present in the source tree. See `LICENSE` and `COPYING`.

## Status

This fork is maintained specifically to extend the useful life of SCCP deployments on newer Asterisk and Linux environments while carrying the fixes needed to keep RTP voice streams working reliably.
