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

## tracepoint vs kprobe

To hook into  syscall, we need to identify the eBPF hook point. This can be done using a tracepoint (i.e. a predefined event directly in the kernel), or a _kprobe_ (a specific kernel function).





## Links

{% embed url="https://www.acceis.fr/introduction-to-ebpf/" %}

{% embed url="https://www.acceis.fr/ebpf-program-creation-in-practice-pid-concealment-part-1/" %}

{% embed url="https://www.acceis.fr/ebpf-in-practice-pid-concealment-part-2/" %}
