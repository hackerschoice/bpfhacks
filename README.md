# eBPF tools

A (short) collecton of eBPF enabled tools (needs root privileges to run);

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
<p align="center">
<img width="675" alt="ptysnoop" src="https://github.com/hackerschoice/bpfhacks/assets/5938498/de068ae5-9cea-44fc-83a6-56e4d37dee93">
</p>
