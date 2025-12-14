# Learning Go - Boot.dev Local Challenges

This repository contains local implementations of Boot.dev Go challenges. Use the provided scripts to set up new challenges and run tests.

## Setting Up a New Challenge

Use the `scripts/new_challenge.sh` script to create a new challenge directory with boilerplate code and tests.

### Usage

```
./scripts/new_challenge.sh <chapter> <NN> "Challenge Title" ["Chapter Title"] [--no-code]
```

- `<chapter>`: Chapter number (e.g., 04 for structs).
- `<NN>`: Challenge number within the chapter (zero-padded, e.g., 01).
- `"Challenge Title"`: Human-readable title for the challenge.
- `"Chapter Title"`: Optional human-readable title for the chapter (e.g., "Structs").
- `--no-code`: Optional flag to skip creating Go code and test files (for multiple-choice questions).

### Examples

- Create a code challenge: `./scripts/new_challenge.sh 04 01 "Structs in Go" "Structs"`
- Create a no-code challenge: `./scripts/new_challenge.sh 04 02 "Multiple Choice Question" --no-code`

This creates a directory like `challenges/04-structs/01-structs-in-go/` with:

- `structs_in_go.go`: Boilerplate Go code.
- `structs_in_go_test.go`: Placeholder tests.
- `README.md`: Challenge description (edit this with instructions from Boot.dev).

## Running Tests

To run tests for a specific challenge:

```
go test ./challenges/<chapter>/<challenge> -v
```

For example:

```
go test ./challenges/04-structs/01-structs-in-go -v
```

- `-v`: Verbose output to see detailed test results.
- Replace `<chapter>` and `<challenge>` with the actual directory names.

For all tests in a chapter:

```
go test ./challenges/<chapter>/... -v
```

## General Go Commands

- Build: `go build ./path/to/file.go`
- Run: `go run ./path/to/file.go`
- Format: `go fmt ./path/to/file.go`
- Mod tidy: `go mod tidy` (to clean up dependencies)

Edit the generated files with your solutions, then run tests to verify!
