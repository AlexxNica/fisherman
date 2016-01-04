fisher-install(1) -- Enable / Install plugins
=============================================

## SYNOPSIS

fisher `install` [*name* or *url* ...] [`--quiet`] [`--help`]

## USAGE

fisher `install` *plugin* ...<br>
fisher `install` *owner/repo* ...<br>

## DESCRIPTION

Install one or *more* plugins by *name*, searching `$fisher_index` or by *url*. If no arguments are given, read the standard input.

If the domain or host is not provided, Fisherman will use any value in `$fisher_default_host`. The default is `https://github.com`.

In addition, all of the following variations are accepted:

* `github`/owner/repo `->` https://github.com/owner/repo<br>
* `gh:`owner/repo `->` https://github.com/owner/repo<br>

Shortcuts for other common Git repository hosting services are also available:

* `bb:`/owner/repo `->` https://bitbucket.org/owner/repo<br>
* `gl:`/owner/repo `->` https://gitlab.com/owner/repo<br>
* `omf:`/owner/repo `->` https://github.com/oh-my-fish/repo<br>

If a copy of the plugin already exists in `$fisher_cache`, the relevant files will be copied to `$fisher_config`/functions, otherwise the plugin repository is first downloaded. If you wish to update a plugin, use `fisher update` *plugin* instead.

If the plugin declares dependencies, these will be installed as well. If any dependencies are already installed they will not be updated in order to prevent version issues. See `fisher help fishfile`#{`Plugins`}.

If a plugin includes either a fish_prompt.fish or fish_right_prompt.fish, both files are first removed from `$fisher_config`/functions and then the new ones are copied.

## OPTIONS

* `-q` `--quiet`:
    Enable quiet mode.

* `-h` `--help`:
    Show usage help.

## PROCESS

Here is a typical install process breakdown for *plugin*:

1. Check if *plugin* exists in `$fisher_index`. Fail otherwise.
2. Download *plugin* to `$fisher_cache` if it is not there already.
3. Copy all `*.fish` and functions/`*.fish` files to `$fisher_config`/functions.
4. Copy all completions/`*.fish` to `$fisher_config`/completions.
5. Copy all man/man[`1-7`] to `$fisher_config`/man/man`%`

Here is the *plugin* tree inside the cache:


`$fisher_cache`/*plugin*<br>
|-- README.md<br>
|-- *plugin*.fish<br>
|-- functions<br>
|   |-- plugin_helper.fish<br>
|-- completions<br>
|   |-- *plugin*.fish<br>
|-- test<br>
|   |-- *plugin*.fish<br>
|-- man<br>
    |-- man1<br>
        |-- *plugin*.1<br>


And thisi is how the files are copied from `$fisher_cache`/plugin to `$fisher_config`:

1. *plugin*.fish `->` $fisher_config/functions
2. functions/plugin_helper.fish `->` $fisher_config/functions
3. completions/*plugin*.fish `->` $fisher_config/completions
4. man/man1/*plugin*.1 `->` $fisher_config/man/man1

## SEE ALSO

`fisher`(1)<br>
`fisher help config`<br>
`fisher help update`<br>
`fisher help uninstall`<br>
`fisher help fishfile`#{`Plugins`}<br>
