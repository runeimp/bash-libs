BASH-Libs
=========

Script Creation
---------------

### BASH It In

`bashitin` is a tool for the creation of new scripts by giving it a script name it will:

1. Initialize a new script file in your personal `bin` directory if you have one setup or one of several standard user `bin` directories.
2. Make the script executable.
3. Open the script in your $VISUAL editor if that environment variable is defined or your $EDITOR otherwise.

#### Usage Example

```
# Create a script named 'example-app'
$ bashitin example-app

# Create a script with the app name of 'Example App' which will result in the script having the slugified CLI name of 'example-app'
$ bashitin --app-name "Example App"

# Create a script with the app name of 'Example App' but the CLI name of 'exapp'
$ bashitin -a "Example App" -c exapp

# Create a script that utlizes /bin/sh instead of /usr/bin/env bash for the bang path
$ bashitin --bang-path "/bin/sh" example-app

```

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
$ chmod +x example-app
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


