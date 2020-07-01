# Module Manager On BASH (MMOB)
Lightweight and easy function manager for BASH

# Script appointment
Make work with custom commands for BASH easier.

# How it works?
First it looks for MDB, Module DataBase files. Module = Function

MDB default structure is:
* functions (your custom commands)
* script DB editing (with addmodule command)

Module structure is:
* name
* description
* command to use module
* id (set up automatically)
* token (set up automatically)

Then it prints module list and it is sourcing mdb files, for functions use.

Done, you can use your custom commands in terminal!

# Why just not .bashrc or ~/bin?
With this script, you can manage your functions and script easier, you will never forget about your command, script prints all commands on start.

# How to create my own MDB?
First, add this header to all custom functions:
```sh
if [ "$1" = "--modulecheck" ]; then
    echo "$(getToken "$FUNCNAME")"
    exit 0
fi
```

Then add addmodule command to put your module to DB:
```sh
addmodule "command" "name" "description"
```

ID and token will be generated automatically.

For example, I created this MDB:
```sh
mysuperfunction() {
    if [ "$1" = "--modulecheck" ]; then
        echo "$(getToken "$FUNCNAME")"
        exit 0
    fi

    echo "hello!!!!!!!"
}

addmodule mysuperfunction "My super module!" "Prints very cool 'hello' word!"
```

Script is searching MDBs with just checking extension on files, MDBs should be with .mdb extension.

# Script usage
```sh
# First start; script will ask you to create configuration file
roman@pc:~$ source mmob
Hello! You have no configuration file for user roman, but we can create it.

Please select option:
[1]: set up a configuration file manually
[2]: use default configuration
[3]: exit from script (default)

mmob> 1
I: starting configurator...
Welcome to mmob configurator! Please follow configurator steps to configure your config file.

Do you want to see debug messages? (Y/n)
Example:
I: debug message

mmob> y
Debug messages were turned on.

Do you want to set custom user token? (leave blank to use generated token)
Token is used to detect module connection with your current mmob session.

mmob> 
Token was set to auto-generated.

Configuration successful! Press any key to exit configurator...
I: Restart script to use your configuration
User token: Z27PRZW2 (cut)
I: cmmob: write 'true' to option 'debug'...
I: cmmob: debug was turned on.
I: ota: checking for updates...
I: checkformdb: found mdb './example.mdb'.
I: addmodule: Starting module DB edit...
I: addmodule: Giving module an ID...
I: addmodule: Module ID: 0
I: addmodule: Module ID: 0
I: addmodule: Module Name: Example 1
I: addmodule: Module Command: hello
I: addmodule: Module Description: Example module for my first MDB
I: addmodule: Module Token: e7c22b994c59d9cf
I: addmoduletodb: adding module 'Example 1' to database...
I: addmoduletodb: adding module 'Example 2' to database...


Module: Example 1
-----------------------------
Description: Example module for my first MDB
Command: hello


Module: Example 2
-----------------------------
Description: Example module 2 for my first MDB
Command: bye


Module: Example 3
-----------------------------
Description: Example module 3 for my first MDB
Command: goodmorning

roman@pc:~$
```

# Reporting bugs
Create an issue for this repository.
