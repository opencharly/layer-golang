# golang

The Go programming language compiler — the `go` toolchain on `PATH`.

`golang` installs the Go compiler/toolchain from each distro's package repo
(arch `go`, debian/ubuntu `golang-go`, fedora `golang-bin`), landing the `go`
driver binary at `/usr/bin/go`. The install is verifiable end to end: the binary
exists, `go version` reports a Go toolchain version, and the toolchain actually
compiles and runs a standalone Go program.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `golang` |
| Distro | all — `go` (arch), `golang-go` (debian/ubuntu), `golang-bin` (fedora) |
| Binary | `go` at `/usr/bin/go` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-image:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-golang:v2026.239.1614'
```

Then, inside the built image:

```bash
go version               # go version goX.Y.Z linux/amd64
go run main.go           # compile and run a program
```

## Layout

- `charly.yml` — the `golang:` candy entity: the per-distro package arms and the
  `check:` steps (including the compile-and-run check).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Family skill: `/charly-coder:golang`
- `/charly-coder:language-runtimes` — a meta-layer that also includes `golang-bin`
- `/charly-internals:go` — the charly CLI is itself built from Go; development conventions
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
