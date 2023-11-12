# eBPF tools

A (short) collecton of eBPF enabled tools (only works as root).

Prerequisite: Install the latest bpftrace tool:
```sh
curl -o bpftrace -fsSL https://github.com/iovisor/bpftrace/releases/latest/download/bpftrace
chmod 755 bpftrace
```

## Sniff all ssh/login/xterm session:

This tools records all PTY sessions and sniffs all ssh/sudo/su passwords of all users.

```
./bpftrace -B none ptysnoop.bt
```

