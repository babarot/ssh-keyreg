ssh-keyreg
===

[![](http://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)][license]

ssh-keyreg is command-line method or programmatically add ssh key to github.com user account.

## Description

>Is there a way to identify with a username and password to github.com servers for the purpose of adding an ssh key to the github user account? So far everything I've read suggests that a user's ssh key must be added via the web GUI. I'm looking for the method or process of adding a key via a command line interface or else a bash/ansible/something script.
> via [command line method or programmatically add ssh key to github.com user account](http://unix.stackexchange.com/questions/136894/command-line-method-or-programmatically-add-ssh-key-to-github-com-user-account)

***DEMO:***

![DEMO](https://raw.githubusercontent.com/b4b4r07/screenshots/master/ssh-keyreg/demo.gif)

## Features

- command-line method add ssh key to github.com
- support bash/zsh

## Usage

```console
$ ssh-keyreg --help
usage: ssh-keyreg [-h|--help][[-d|--desc <desc>][-u|--user <user[:pass]>][-p|--path <path>]] [github|bitbucket]
    command line method or programmatically add ssh key to github.com user account

options:
    -h, --help   show this help message and exit
    -d, --desc   description of registration
    -u, --user   username and password (user:pass)
    -p, --path   path of public key

MIT @b4b4r07 <https://github.com/b4b4r07>
```

For example, this is a basical usage below.

```console
$ cd ~/.ssh; ssh-keygen
$ ssh-keyreg --path id_rsa.rub github
```

## Installation

### Using [Antigen](https://github.com/b4b4r07/zplug) for zsh user

```console
$ zplug "b4b4r07/ssh-keyreg", as:command, use:bin
$ zplug install
```

### Antigen-free install

To install this tool without Antigen:

```console
$ sudo sh -c "curl https://raw.githubusercontent.com/b4b4r07/ssh-keyreg/master/bin/ssh-keyreg -o /usr/local/bin/ssh-keyreg && chmod +x /usr/local/bin/ssh-keyreg"
```

ssh-keyreg is a shell script, so put it somewhere and make sure it's added to your `$PATH`.

## License

[MIT][license] © BABAROT (a.k.a. [b4b4r07](http://b4b4r07.com))

[license]: http://b4b4r07.mit-license.org
