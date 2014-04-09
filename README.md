# git-multi-tools

## What is it?

A set of utilities for managing multiple git repositories in a single project

```
    project
      |
      |-- repo1
      |
      |-- repo2
      |
      |-- repo3
```

## Installation

Either copy or symlink the contents of git-multi-tools/bin (see caveat about realpath below) to a directory in your $PATH (Preferred),

OR Add the path to git-multi-tools/bin to your $PATH


## Multi-Tools

### dir-status

Usage: `git dir-status \[opt: -v\] \[opt: target directory\]`

NOTE: If a target directory is not specified, $PWD is used.

Example output if run from the project directory with no arguments:

```
:~/project $ git dir-status 
Status of repos in /Users/me/project

REPOSITORY              VERSION  BRANCH  STATUS
repo1                   1.3.5    master  dirty
Changed:
  index.js
  serverapp/routes.js
  template_config.yaml
2 clean repos
```

Example with -v (verbose) option:

```
:~/project $ git dir-status -v

Status of repos in /Users/me/project

REPOSITORY                 VERSION  BRANCH   STATUS
repo1                      1.3.5    master   dirty
Changed:
  index.js
  serverapp/routes.js
  template_config.yaml
repo2                      0.4.1    master   clean
repo3                      0.2.1    staging  clean
```

### update-clean

Usage: git update-clean \[opt: target directory\]

NOTE: If a target directory is not specified, $PWD is used.

Example output:

```
:~/project $ git update-clean 

Updating clean repos in /Users/me/project

REPO    VERSION  BRANCH   RESULT
repo1   0.2.1    master   Up to date!
repo2   0.4.1    master   **dirty** Not updated.
repo3   0.2.1    staging  Branch updated! Diff: 1d5ecda..5527a8f
```

## Helpers

 - **current-branch**
   Usage: `git current-branch`
   Active git branch in the current directory

 - **getversion**
   Usage: `getversion`
   Retrieves version from package.json files and git tags that conform to `/^v\[0-9\]+\./`

 - **isclean**
   Usage: `git isclean [opt: -q]`
   Output: By default "clean", if clean, else "dirty"; Silent if -q is passed
   Exit status is 0 if clean, 1 if dirty

 - **realpath**
   Usage: `realpath <relative or absolute path>`
   A workaround for systems that don't have realpath natively (ie, Mac OS).
   Don't put this in your path, if you already have realpath.