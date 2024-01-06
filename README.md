# tree-sitter-roc
Roc grammar for tree-sitter. Forked from [faldor20/tree-sitter-roc](https://github.com/faldor20/tree-sitter-roc)

## References
* [Tree-sitter Introduction](https://tree-sitter.github.io/tree-sitter/)
* [Roc](https://www.roc-lang.org/)

## Installation
### Helix
Example configuration.  See [Adding new languages to Helix](https://docs.helix-editor.com/guides/adding_languages.html)
```toml
[language-server.roc-ls]
command = "roc_lang_server"

[[language]]
name = "roc"
scope = "source.roc"
injection-regex = "roc"
file-types = ["roc"]
shebangs = ["roc"]
roots = []
comment-token = "#"
language-servers = ["roc-ls"]
indent = { tab-width = 2, unit = "  " }

[language.auto-pairs]
'(' = ')'
'{' = '}'
'[' = ']'
'"' = '"'
[[grammar]]

name = "roc"
source.git = "https://github.com/adkelley/tree-sitter-roc"
source.rev = "<<sha hash of the latest commit goes here>>"
```

After updating your `language.toml` file.  Do the following:

1. Build up on the shell
```
$ hx -g fetch
$ hx -g build
```

2.  Make a queries directory and copy the query files to this directory.  
```
$ mkdir -p $HELIX/runtime/queries/roc # make your queries directory for roc
$ cp -r $HELIX/runtime/grammars/sources/roc/queries $HELIX/runtime/queries/roc
```
Note `$HELIX` typically points to `~/.config/helix`

### Neovim
Add the code in `neovim/roc.lua` to your config somewhere.
Copy the folder `neovim/queries` to your neovim config at `after/` or in a custom neovim plugin at its root directory `./`
eg: `after/queries/roc/highlights.lua`or `my_roc_plugin/queries/roc/highlights.lua`

### Emacs
A [package providing a major mode for Roc](https://gitlab.com/tad-lispy/roc-mode "Emacs Roc mode") is under development.
## Contributing
### Setup
Creating language parsers is not for the faint of heart.  However, if you must, see [Creating parsers](https://tree-sitter.github.io/tree-sitter/creating-parsers) to get started.

You will need:
1. The tree-sitter cli, which will be installed when you run `npm install`
2. A c compiler like gcc or clang

### Running
Once you've made a change, to test it, run:
```bash
tree-sitter generate
tree-sitter test 
```
If you add a new feature you should add a test to one of the test files in `test/corpus/*.txt`
once you are happy with you changes run 

```bash
tree-sitter test --update
```
and it will update the test files with your new parsed tree


