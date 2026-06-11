<img src="https://drop.samespace.com/hylyx-og.png" />



# hylyx

**Linux — Built for Apple Silicon.**

Near-native performance. Run in seconds.

*If you love Mac but live in Linux, Hylyx is for you.*

---

## Install

```bash
curl -fsSL https://origon.ai/hylyx/install.sh | bash
```

Requirements: macOS 13+, Apple Silicon.

---

## Why Hylyx?

Running Linux on a Mac shouldn't mean a 3GB download and a daemon squatting on your machine forever.

Hylyx does it differently — a tiny stateless binary, custom kernels stripped to the bare essentials, and optimized images that boot in under two seconds. Native Apple Silicon performance via Virtualization.framework.

Resize disks. Bridge networks. Share directories. All with clean, obvious CLI flags.

No config files. No background processes.

**Just Linux — the way it should be.**

---

## Quick Start

```bash
hylyx install ubuntu   # or alpine, fedora
# SSH key auto-injected, VM starts, shows: ssh root@192.168.64.x

hylyx stop ubuntu      # shutdown
hylyx start ubuntu     # start again
```

---

## Features

- **Native Apple Silicon virtualization** — Built on Apple's Virtualization Framework. No emulation. No legacy overhead.
- **Instant boot** — From download to working Linux shell in under 30 seconds.
- **Ultra-small Linux images** — Ubuntu (78 MB), Fedora (65 MB), Alpine (13 MB).
- **Disk resize** — Grow or shrink VM disks on the fly.
- **Bridged networking** — Bridge VMs to your local network, or use NAT (default).
- **Clone VMs** — Duplicate any stopped VM in seconds.
- **Directory sharing** — Mount host directories inside the VM via virtio-fs.
- **Autostart** — VMs can start automatically when your Mac boots.
- **Fully open-source** — No black boxes. Kernel choices and tooling fully visible.

---

## Commands

```
hylyx                         Show VMs and status
hylyx install <name> [distro] Create VM, copy SSH, start
hylyx start <name>            Start in background
hylyx start <name> -c         Start with serial console
hylyx stop <name> ...         Stop VM(s)
hylyx restart <name> ...      Restart VM(s)
hylyx del <name> ...          Delete VM(s)

hylyx info <name>             Show details, discover IP
hylyx clone <src> <dst>       Clone stopped VM
hylyx resize <name> <GB>      Grow or shrink disk
hylyx autostart <name>        Enable boot startup (sudo)
hylyx autostart <name> off    Disable boot startup (sudo)

hylyx images [filter]         List available images
hylyx bridges                 List network interfaces
hylyx update                  Update Hylyx
hylyx uninstall               Remove Hylyx
hylyx help                    Show help
```

---

## Install Options

```
-p <n>       CPU cores (default: all)
-m <GB>      Memory (default: 2)
-s <GB>      Disk size (default: 16)
-b <iface>   Bridge network (default: NAT)
-d <path>    Mount host directory (mount -t virtiofs host /mnt)
-t <file>    Use local rootfs archive
```

Example:
```bash
hylyx install myvm ubuntu -p 4 -m 8 -s 50
```

---

## Documentation

Full docs at [origon.ai/hylyx/docs](https://origon.ai/hylyx/docs/)

---

## Build from Source (macOS)

```bash
./build.sh
```

This compiles the Swift binary, bundles e2fsprogs, codesigns, and optionally notarizes.

---

## Building Kernel & Images

> ⚠️ **Must be built on a Linux machine** (not macOS)

The `linux/` folder contains scripts to build the custom kernel and VM images.

**Requirements:** Linux host with root access, `aarch64-linux-gnu-` cross-compiler.

```bash
cd linux

# Build custom Linux kernel (arm64)
make linux

# Build VM images
make ubuntu    # Ubuntu 26.04
make alpine    # Alpine 3.23
make fedora    # Fedora 43
```

Output: `linux/images/`

---

## License

MIT
