# AGENTS.md — layer-golang

Standalone candy repo for the `golang` layer — the Go compiler/toolchain from
each distro's package repo, landing `go` at `/usr/bin/go`. The candy lives in
`charly.yml` at the repo root and projects the `golang` skill entity
(`family: coder`).

Canonical files:

- `charly.yml` — the `golang:` candy entity and the `golang-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-coder:golang` — the owning skill: the per-distro package names, the
  `go version` check, and the compile-and-run check. Load before editing or
  troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package
  sections). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: the `/usr/bin/go`
  file check, the `go version` stdout match, the standalone compile-and-run
  check (`charly-go-build-ok`), and the `package=go` check with its
  `package_map`.
- This is a dependency candy for Go-based tools (e.g. `layer-gifgrep`,
  `layer-gogcli`); the toolchain it lands is what they compile with.

## Modify this repo

- Edit the `golang:` candy entity in `charly.yml`; keep the matching
  `golang-skill:` entity in step with it.
- Keep the `package_map` in the `package=go` check aligned with the per-distro
  package arms — a package rename on a distro is a change in both places.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
