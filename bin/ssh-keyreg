#!/bin/bash
# Author:  BABAROT (@b4b4r07)
# License: MIT License

# references
# * {http://unix.stackexchange.com/questions/136894/
#    command-line-method-or-programmatically-
#    add-ssh-key-to-github-com-user-account
#   }
# * {https://github.com/ABCanG/add-sshkey-remote}

die() {
    echo "$@" >&2
    exit 1
}

usage() {
    cat <<HELP
usage: ${0##*/} [-h|--help][[-d|--desc <desc>][-u|--user <user[:pass]>][-p|--path <path>]] [github|bitbucket]
    command line method or programmatically add ssh key to github.com user account

options:
    -h, --help   show this help message and exit
    -d, --desc   description of registration
    -u, --user   username and password (user:pass)
    -p, --path   path of public key

MIT @b4b4r07 <https://github.com/b4b4r07>
HELP
}

while (($# > 0)); do

    # check flags and arguments
    case "$1" in
        -h|--help)
            die "$(usage)"
            ;;

        -d|--desc)
            [[ -z $1 ]] && die "$1: require arguments"
            desc="$2"; shift;
            ;;

        -u|--user)
            [[ -z $1 ]] && die "$1: require arguments"
            user="$2"; shift;
            ;;

        -p|--path)
            [[ -z $1 ]] && die "$1: require arguments"
            path=~/.ssh/"${2##*/}"; shift
            ;;

        github)
            servies="github"
            ;;

        bitbucket)
            servies="bitbucket"
            ;;
    esac
    shift
done

desc="${desc:-$(date +%D)}"
user="${user:-$(git config --get user.name)}"
path="${path:-$HOME/.ssh/id_rsa.pub}"
title="$(hostname) ($desc)"

# check if the path is available
[[ -f $path ]] || die "$path: no such file or directory"
key_data="$(cat "$path")"

case "$servies" in
    ""|github)
        result="$(
        curl -u "${user:=$USER}" \
            --data "{\"title\":\"$title\",\"key\":\"$key_data\"}" \
            https://api.github.com/user/keys
        )"
        ;;

    bitbucket)
        result="$(
        curl -u "${user:=$USER}" \
            --data "label=$label" \
            --data-urlencode "key=$key_data" \
            https://bitbucket.org/api/1.0/users/"${user%:*}"/ssh-keys
        )"
        ;;
esac

# check if upload is completed successfully
ssh -T git@github.com 2>&1 | grep "success"
if [[ $? -ne 0 ]]; then
    die "sorry, try again"
fi
