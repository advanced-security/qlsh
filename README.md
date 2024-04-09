# qlsh - a CodeQL REPL shell

> [!WARNING]
> This is an _unofficial_ tool created by Field Security Specialists, and is not officially supported by GitHub.

qlsh is a simple shell for running [CodeQL](https://codeql.github.com/) queries against a database.

It lets you write and run queries interactively in a REPL, and see the results immediately.

> [!WARNING]
> This is an _unofficial_ tool created by Field Security Specialists, and is not officially supported by GitHub.

## Usage

```bash
qlsh /path/to/codeql-database
```

Get help with:

```bash
qlsh
```

The language of the database is autodetected, and any required language packs are downloaded for you.

If the database is bundled it will be extracted into a temporary directory.

At the prompt, you can run queries and see the results immediately after a "select " statement is entered.

Any lines not starting with "select " and that are not recognised as a REPL command are added to the current CodeQL query.

Here's an example of using the REPL to run a query:

```bash
$ qlsh /path/to/codeql-database
codeql> select "Hello, world!"
|     col0      |
+---------------+
| Hello, world! |
codeql> quit
$ 
```

Here's a slightly longer example on a Java database:

```bash
$ qlsh /path/to/codeql-database
codeql> from Expr expr
... where expr.getLocation().getFile().getBaseName() = "Main.java"
... select expr
|      expr       |
+-----------------+
| void            |
| ...[]           |
| String          |
| println(...)    |
| System.out      |
| "Hello, World!" |
| 0               |
codeql> quit
$ 
```

Commands:

* `quit` - exit the shell (you can also use Control-D)
* `help` - show the help message
* `show` - show the current query
* `reset` - clear the current query (you can also use Control-C)

## Requirements

* CodeQL CLI: [binary release](https://github.com/github/codeql-cli-binaries/releases) or [Actions bundle](https://github.com/github/codeql-action/releases)
* bash
* jq
* rlwrap (optional, for readline support)
* a CodeQL database, for a codebase you are [licensed to analyze](https://github.com/github/codeql-cli-binaries/blob/main/LICENSE.md)

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
