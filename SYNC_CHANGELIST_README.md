# Deploy multiple Git repositories in an unique folder

`modgit` is a shell script for deploying multiple Git repositories in root folder of any project, which is not possible with default `git submodule` command. A common use case would be the easy installation of Magento modules that need to be deployed in root folder. 

This version can (sync) copy/remove only affected files rather than removing all files then adding back.

Disclaimer: Use at your own risk! Test it before using anywhere near a production system. The original author [https://github.com/jreinke](https://github.com/jreinke "jreinke") has not endorsed and does not support this version!

## Installation

### curl installation

    $ curl https://raw.githubusercontent.com/adrian-green/modgit/develop/modgit > modgit
    $ chmod +x modgit
    $ sudo mv modgit /usr/local/bin

### wget installation

    $ wget -O modgit https://raw.githubusercontent.com/adrian-green/modgit/develop/modgit
    $ chmod +x modgit
    $ sudo mv modgit /usr/local/bin

### Manual download
* Download shell script [here](https://raw.githubusercontent.com/adrian-green/modgit/develop/modgit)
* Copy modgit file to `/usr/local/bin` (or any folder in your $PATH)
* Run `chmod +x modgit`

## Usage

### Install a module

    $ cd /path/to/project
    $ modgit init
    $ modgit add [-n] [-t tag_name] [-b branch_name] <module> <git_repository>

### Update a module

    $ modgit up [-n] <module>

### Update all modules

    $ modgit up-all [-n]

### Sync a module

    $ modgit sync [-n] <module>

### Sync all modules

    $ modgit sync-all [-n]

### Remove a module

    $ modgit rm [-n] <module>

### Remove all modules

    $ modgit rm-all [-n]

### List installed modules

    $ modgit ls

### Show information about an installed module

    $ modgit info <module>

### Show deployed files of an installed module

    $ modgit files <module>

### Show help

    $ modgit help

## Advanced usage

### Dry run mode

    $ modgit add -n scheduler https://github.com/fbrnc/Aoe_Scheduler.git
      => show what would be done

### Include filter

    $ modgit add -i lib/ elastica git://github.com/ruflin/Elastica.git
      => will deploy only lib/ folder

### Include filter with custom target

    $ modgit -i lib/:library/ add elastica git://github.com/ruflin/Elastica.git
      => will deploy only lib/ (remote folder) to library/ (local folder)

### Exclude filter

    $ modgit add -e tests/ atoum https://github.com/atoum/atoum.git
      => will deploy all remote files and folders, except tests/ folder

### Automatic modman compatibility

    $ modgit add debug https://github.com/madalinoprea/magneto-debug.git
      => will parse remote modman file for files and folders mapping
