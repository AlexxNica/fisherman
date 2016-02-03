fisher-fishfile(5) -- Fishfile Format
=====================================

## SYNOPSIS

A *fishfile* lets you share plugin configurations across multiple installations, allows plugins to declare dependencies, and prevent information loss in case of system failure.

Fisherman also keeps a user *fishfile* in `$fisher_file` which is automatically updated as you install or uninstall plugins.

## USAGE

Fishfiles are plain text, manifest files that list one or more plugins by their name, URL or path to a local project.

Here is an example:

```
# my plugins
shark
fishtape

# other links
oh-my-fish/bobthefish
```

To read fishfiles use `fisher --file=fishfile`. This will read *fishfile* sequentially, writing its contents to the standard output. Oh My Fish! bundle files are supported as well.

If *fishfile* is null or an empty string, the global *fishfile* in `$fisher_file` will be used. Use a dash `-` to force read from standard input.

## PLUGINS

Plugins may declare any number of dependencies to other plugins in a fishfile at the root of their project.

By default, when Fisherman installs a plugin, it will also fetch and install its dependencies. If a dependency is already installed, it will not be updated as this could potentially break other plugins using an older version. For the same reason, uninstalling a plugin does not remove its dependencies.

To understand this behavior, it helps to recall the shell's single scope for functions. The lack of private functions means that, it is *not* possible to single-lock a specific dependency version. See also `Flat Tree` in `fisher help tour`.

## SEE ALSO

fisher(1)<br>
fisher help config<br>
