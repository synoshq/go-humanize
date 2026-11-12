# go-humanize — agent guide

Formatters that turn numbers, sizes and times into human-friendly strings (`Bytes`, `Comma`,
`Ordinal`, `Time`, `SI`, ...). Pure Go, no dependencies.

## Layout

- Core formatters: `bytes.go`, `comma.go`, `commaf.go`, `ftoa.go`, `number.go`, `ordinals.go`,
  `times.go`.
- `english/`, `si.go`, `bigbytes.go`, and `big.go` are normally synced from the upstream
  unit-formatting module. Keep changes there minimal and compatible with upstream; do not make
  unrelated edits or generated-file churn.

## Working rules

- Keep changes small and focused on the reported problem.
- When a failing test demonstrates a defect, fix the implementation, including synced code when
  necessary, rather than changing a correct expected value to match defective behavior.
- Expected values in `*_test.go` are golden outputs. Update one only when the requested or
  established behavior has intentionally changed.
- Do not run `go test` locally; the suite is slow and CI runs it on every push. Use `go build ./...`
  and `go vet ./...` to check your change compiles.
- Keep code gofmt-formatted.

## Tooling policy

- Change files only with the editor's edit tools. Shell commands that write or move files (`cp`,
  `mv`, `sed`, `tee`, shell redirects, scripting interpreters) and all `git` commands are blocked by
  `.cursor/cli.json`; the harness files (`AGENTS.md`, `.cursor/`) are read-only.
