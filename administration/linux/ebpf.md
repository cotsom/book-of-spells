# eBPF

## Hooks

**eXpress Data Path (XDP)** - network packet processing

**kprobe** - syscool processing

**tracepoints -** A TC program is similar to XDP. The main difference is that it runs a bit later in the networking stack. It also can run on packet ingress and egress. The benefit to running later in the networking stack is that it offers more context around the packet. This allows more data to be gathered about the packet and where it’s headed.

## vmlinux.h

You can create the `vmlinux.h` file using the `bpftool`, which is a necessary utility for eBPF tasks.

```bash
bpftool btf dump file /sys/kernel/btf/vmlinux format c > vmlinux.h
```

