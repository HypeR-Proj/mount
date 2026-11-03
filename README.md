<!--
SPDX-FileCopyrightText: 2026 roolrz
SPDX-License-Identifier: Apache-2.0
-->

# mount

Filesystem manager client for listing and mounting Native volumes.

Encodes mount commands using `lib-service` and sends them to fs-backend. It does not
receive raw block-device authority. The manager selects a format worker and owns mount
publication.

See the [implementation entry](src/main.rs) and [component declaration](component.json)
for the public interfaces, build dependencies and delivered artifacts.

## Usage

In a Native session with the required capabilities:

```sh
mount
mount --help
```

## Boundaries

The default table is /etc/fstab. Supported explicit formats are auto, fat, erofs and
f2fs; available workers and source authority depend on deployment. Use `mount -a` only
when intending to mount the table entries.

## Build and test

Use this checkout inside the [repo-managed workspace](https://github.com/HypeR-Proj/HypeR).
From this repository directory:

```sh
make
make test
```

An absolute `OUT=/path/to/out` selects a shared output directory. The module
entry delegates to build/system, which prepares the installed SDK and declared
dependencies. Native binaries require HypeR; host module checks cover the tests
selected by component.json. A standalone clone does not contain the workspace’s
other source repositories or Native SDK.
