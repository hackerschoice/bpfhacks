# eBPF tools

A (short) collecton of eBPF enabled tools (need root privileges to run);

Prerequisite: Install the latest bpftrace tool:
```console
curl -o bpftrace -fsSL https://github.com/iovisor/bpftrace/releases/latest/download/bpftrace
chmod 755 bpftrace
```

## Project #1 - Sniff all ssh/login/xterm session:

Record all PTY sessions and sniffs all ssh/sudo/su passwords of all users.

```console
export BPFTRACE_STRLEN=200
./bpftrace -Bnone ptysnoop.bt
```
<p align="center">
<img width="675" alt="ptysnoop" src="https://github.com/hackerschoice/bpfhacks/assets/5938498/de068ae5-9cea-44fc-83a6-56e4d37dee93">
</p>

Tools by others: [SSHLog](https://ebpf.io/applications/#sshlog).

## Project #2 - Keylogger:

Record all keys pressed on the keyboard:

```console
./bpftrace -Bnone keylogger.bt
```
<p align="center">
<img alt="keuylogger" src="https://github.com/hackerschoice/bpfhacks/assets/5938498/2d9d90bf-497d-4cc7-9583-5b8c162231b6">
</p>

## TIPS & TRICKS

It may complain about missing Linux Kernel header files. Download them to a local directory:
```sh
wget https://debian.sipwise.com/debian-security/pool/main/l/linux/linux-headers-...
dpkg-deb -xv linux-headers-*.deb "$(pwd)"
export BPFTRACE_KERNEL_SOURCE="$(echo "$(pwd)/usr/src/linux-headers-"*)"
sed '/generated\/autoconf.h/d' -i "${BPFTRACE_KERNEL_SOURCE}/include/linux/kconfig.h"
```

Check for BPF support in the Kernel (it is enabled by default):
```sh
grep CONFIG_BPF /boot/config-$(uname -r)
```


