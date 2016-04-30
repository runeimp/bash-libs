BASH-Libs
=========

Option Parsing
--------------

### BASH Subcommand Processing

Git style subcommands.

Library
: `bashsubimp.shlib`

#### Usage Example

```
$ cd ~/bin
$ touch example-app
$ $EDITOR example-app
```

In your editor put:

```
#!/usr/bin/env bash

APP_AUTHOR="RuneImp"
APP_CLI="example-app"
APP_LICENSE="MIT"
APP_NAME="Example App"
APP_VERSION="0.1.0"
APP_LABEL="${APP_AUTHOR}'s $APP_NAME v${APP_VERSION}\nLicense: $APP_LICENSE"

# export DEFAULT_LIST_SUBCOMMANDS=1

source bashsubimp.shlib

```

Then on the command line you can do:

```
$ example-app version
0.1.0
$ example-app Version
RuneImp's Example App v0.1.0
License: MIT
$ example-app list
  Example App Commands:
    list         List all subcommands.
    version      Display application version number only.
    Version      Display application label with version number.
$ example-app
  Example App Commands:
    list         List all subcommands.
    version      Display application version number only.
    Version      Display application label with version number.
```

If you uncomment the `export DEFAULT_LIST_SUBCOMMANDS=1` line in `example-app` the default behavior for calling your app without a subcommand becomes:

```
$ example-app
  ERROR: No command specified
```

Remember in shell scripting `0` is `true` and `1` or more is `false`. `DEFAULT_LIST_SUBCOMMANDS` defaults to `0`.

And when you do create a subcommand and then call list:

```
$ echo "#!/usr/bin/env bash\necho 'example-app-test called!'" > example-app-test
$ chmod +x example-app-test
$ example-app list
  Example App Commands:
    list         List all subcommands.
    version      Display application version number only.
    Version      Display application label with version number.
    test
$ example-app test
example-app-test called!
```

### ToDo

* [ ] Setup help system to populate the command list with descriptions.
* [ ] Fix command sorting with default commands intersperced properly.


