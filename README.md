# qlsh - a CodeQL REPL shell

qlsh is a simple shell for running CodeQL queries against a database.

It lets you write and run queries interactively in a REPL, and see the results immediately.

## Requirements

- CodeQL CLI
- a CodeQL database, for a codebase your are [licensed to analyze](https://github.com/github/codeql-cli-binaries/blob/main/LICENSE.md)
- bash
- jq
- rlwrap

## Installation

It's just a bash script, so you can download it and run it from anywhere, such as your `.local/bin` directory, if that's on your `PATH`:

```bash
cp qlsh ~/.local/bin
```

You can also add an alias to your shell configuration:

Bash:
```bash
echo 'alias qlsh="/path/to/qlsh/qlsh"' >> ~/.bashrc
```

Zsh:
```zsh
echo 'alias qlsh="/path/to/qlsh/qlsh"' >> ~/.zshrc
```
