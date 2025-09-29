# Installing and creating a new toolkit

You can run this in your terminal to install a toolkit called kalvin-toolkit and run its commands with `kt *` or `k *` (can change later via config file)
(You can also look at that raw file to see what it does):

```
wget https://raw.githubusercontent.com/neitanod/bash-toolkit/refs/heads/main/setup-kalvin-toolkit && source ./setup-kalvin-toolkit
```


It's basically a file I made for you that is in the repo but should actually be in a gist or something, as it itself clones the repo.

It first clones the repo, then it creates a toolkit for you, then puts some sample scripts and autocompleters in it.

Then you can `kt <tab>`  or `k <tab>` to list the scripts, and also `k selected-script-name <tab>` to get autocompletion for positional commands, and `k selected-script-name --<tab>` to get autocompletion for `--something= modifiers` .


# Creating a new command


## Shortcut to creating a new empty command

and you can quickly create a new command with `k command-name-here ---edit` (that would also edit it if it already exists)

`---edit` (three hyphens) is a meta-modifier for your commands in the toolkit. It opens the script in your editor for you to edit it.


## Creating a new command with a scaffold

You can also create a non-empty, scaffolded new command with a command like:

```
k create-command command-name-here --signature="my_positional_command_1 my_positional_command_2 --my-flag|-m --my-flag-with-default|-d=default_value"
```

That will create a script by that name with the argument parser in place and automatically build and show the help message when that command is called with --help|-h or with missing required arguments.

Once the scaffolded script gets created, you can edit it with `k command-name-here ---edit` and put the actual functionality at the bottoms, replacing the placeholder echoes it has.

## Creating and editing autocompletion commands for existing commands

Then you can create autocompletion scripts in the folder bin/autocomplete/ with the name `command-name-here_1` and it will be automatically used when you run `k command-name-here <tab>` or `kt command-name-here <tab>` 

```
bin/autocomplete/command-name-here_1  # will be used for the first positional argument
bin/autocomplete/command-name-here_2  # will be used for the second positional argument
bin/autocomplete/command-name-here_flags  # will be used for selecting the available flags
bin/autocomplete/command-name-here_flag-name  # will be used for the flag --flag-name=<values>
bin/autocomplete/command-name-here_another-flag  # will be used for the flag --another-flag=<values>
```

Commands created with `k create-command` can provide their own `_flags` autocompleter.

You can run this:

```
kt create-command-flags-autocomplete create-command
kt create-command-flags-autocomplete create-command --edit   # will open the file it just created
```

It will create a file `bin/autocomplete/create-command_flags` that will provide autocompletion for the flags of the `create-command` command simply by running:

```
kt create-command ---flags
```


Another example: 

```
k create-command-flags-autocomplete create-command-flags-autocomplete
k create-command-flags-autocomplete create-command-flags-autocomplete --edit   # will open the file it just created
```

Will do the same for the create-command-flags-autocomplete command itself, adding autocomplete for --force at al.






