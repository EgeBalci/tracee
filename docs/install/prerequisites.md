# Prerequisites

Portable (CO:RE) option:
- Linux kernel version >= 4.18
- BTF enabled (_You can manually detect if your environments supports it by checking if the following file exists on your machine: /sys/kernel/btf/vmlinux or consult the following documentation: https://github.com/libbpf/libbpf#bpf-co-re-compile-once--run-everywhere_)

Kernel version specific option:
- Linux kernel version >= 4.18
- Linux kernel headers available under conventional location (see [Linux Headers](../headers) section for more info)
- libc, and the libraries: libelf, zlib
- GNU Make >= 4.3
- clang >= 11
Exceptions:

- Tracee supports loading a pre-compiled eBPF file, in which case the kernel headers are not required at runtime, but only for the one-time compilation of the eBPF program. See [Setup Options](../ebpf-compilation) for more info.
- When using Tracee's Docker image, all of the tooling is built into the image. The only requirement left is the kernel headers or the pre-built eBPF artifact. See [Setup Options](../ebpf-compilation) for more info.

# Permissions

For using the eBPF Linux subsystem, Tracee needs to run with sufficient capabilities: 
- `CAP_SYS_RESOURCE` (to manage eBPF maps limits)
- `CAP_BPF`+`CAP_TRACING` which are available on recent kernels (>=5.8), or `SYS_ADMIN` on older kernels (to load and attach the eBPF programs).

Alternatively, run as `root` or with the `--privileged` flag of Docker.
