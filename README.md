# Simple test ebpf-go program

See [https://ebpf-go.dev/guides/getting-started/](https://ebpf-go.dev/guides/getting-started/)

## Requirements:

- kernel 5.7 and up for bpf_link
- `clang`, optional `clang-tools-extra` (fedora)
- llvm-strip (`llvm`)
- `libbpf-dev` (debian/ubuntu), `libbpf-devel` (fedora)
- kernel headers. `kernel-devel` (fedora)
- golang compiler for ebpf-go module

## Overview
Sample network interface packets counter. 

C source file should have top directive `//go:build ignore` to be ignored by golang compiler. `go gen` generates additional scaffolding **.go** files **counter_bpfeb.go** and **counter_bpf_el.go** along side with object files.

## Usage

1. Init module
```console
$ go mod init ebpf-test
```

2. Add sums and requirements
```console
$ go mod tidy
```

3. Get dependency 
```console
$ go get github.com/cilium/ebpf/cmd/bpf2go
```

4. Generate (make sure *gen.go* has EOL)
```markdown
$ go generate
```
5. Update, if needed, network interface *eth0* in **main.go** to any is active on local machine (check via `ifconfig`)

6. Compile and run
```console
$ $ go build && sudo ./ebpf-test
```
### Output

```console
2024/10/06 15:05:27 Counting incoming packets on eth0..
2024/10/06 15:05:28 Received 1 packets
2024/10/06 15:05:29 Received 2 packets
2024/10/06 15:05:30 Received 3 packets
...
```

7. For iterations, use
```console
$ go generate && go build && sudo ./ebpf-test
```

## See also

```console
$ man bpf
```
