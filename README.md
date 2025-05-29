# qlsh - a CodeQL REPL shell

> [!NOTE]
> This is an _unofficial_ tool created by Field Security Specialists, and is not officially supported by GitHub.

qlsh is a simple shell for running [CodeQL](https://codeql.github.com/) queries against a database.

It lets you write and run queries interactively in a REPL, and see the results immediately.

> [!NOTE]
> This is an _unofficial_ tool created by Field Security Specialists, and is not officially supported by GitHub.

## Usage

```bash
qlsh /path/to/codeql-database
```

Get help with:

```bash
qlsh
```

The language of the database is autodetected, and any required language packs are downloaded for you from GitHub.com servers.

If the database is bundled it will be extracted into a temporary directory. For large databases, this can take a while. You may prefer to extract the database yourself and pass the path to that.

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
* `help <search term>` - search CodeQL online library for provided terms, backed by AddSearch (see [Privacy](#privacy))
* `show` - show the current query
* `reset` - clear the current query (you can also use Control-C)
* `lang` - show the database language
* `dir` - show the current query's temporary directory

## Requirements

* CodeQL CLI
  * You can get this by one of:
    * The [CodeQL CLI](https://cli.github.com/) with the CodeQL CLI extension installed with `gh extensions install github/gh-codeql`
    * Install on MacOS with `brew install codeql`
    * [binary release](https://github.com/github/codeql-cli-binaries/releases)
    * [Actions bundle](https://github.com/github/codeql-action/releases)
* `bash`
* `jq`
* a CodeQL database, for a codebase you are [licensed to analyze](https://github.com/github/codeql-cli-binaries/blob/main/LICENSE.md)

Optional:

* `rlwrap` for readline support
* `curl` for online help
* `lynx` for showing online help

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

## License

This project is licensed under the terms of the MIT open source license. Please refer to the [LICENSE](LICENSE) for the full terms.

This tool uses the `codeql` binary, for which you must separately accept the [license to use](https://github.com/github/codeql-cli-binaries/blob/main/LICENSE.md).

## Maintainers

See [CODEOWNERS](CODEOWNERS) for the list of maintainers.

## Support

> [!NOTE]
> This is an _unofficial_ tool created by Field Security Specialists, and is not officially supported by GitHub.

See the [SUPPORT](SUPPORT.md) file.

## Privacy

This tool uses the `codeql` binary. That tool can communicate with GitHub servers to perform its functions - in this case, to download required language packs. See [PRIVACY](PRIVACY.md) for a link to the GitHub General Privacy Statement.

The `help <keyword>` function uses the same service as used by the [CodeQL docs website](https://codeql.github.com/docs/), which is hosted by [AddSearch](https://www.addsearch.com/) and subject to their [privacy notice](https://www.addsearch.com/privacy/).

## Background

See the [CHANGELOG](CHANGELOG.md), [CONTRIBUTING](CONTRIBUTING.md), [SECURITY](SECURITY.md), [SUPPORT](SUPPORT.md), [CODE OF CONDUCT](CODE_OF_CONDUCT.md) and [PRIVACY](PRIVACY.md) files for more information.
