# git-manage
Local git server repository management scripts.

The intent of this project is to simplify the management of a local git server, specifically a server that is mirroring repositories from GitHub.

Two scripts are provided: **clone** and **pull**. 

All file operations are relative to the location of the scripts unless the `-r` option is used to indicate a different root directory. The scripts are intended to live in the server's git storage directory.

## Clone

The **clone** script uses the `git clone` command to clone specified repositories onto the server. Several options are available to select repositories as shown in the examples below. 

Use the `-i` option to pull information about the specified repositories instead of cloning them. Information is pulled from the GitHub API and is output in json format. The information option can be especially powerful when paired with the [jq](https://github.com/stedolan/jq) utility. An optional GitHub API authentication token can be specified with the `-t` option. The token option is especially useful when making more information requests than the standard API limit.

### Examples

Clone from a single url:
```
./clone https://github.com/otisbyron/git
```

Clone a list of urls from a file:
```
./clone -f git_urls.list
```

Clone all repositories for a specific user:
```
./clone -u markqvist
```

Get the number of stars for a repository:
```
./clone -i https://github.com/ansible/ansible | jq '.stargazers_count'
```

Capture information on all repositories for a specific organization:
```
./clone -i -o unitedstates > git_unitedstates.info
```

See the full help text for the script:
```
./clone -h
```

## Pull

The **pull** script uses the `git pull` command to pull the latest version of the specified repositories.

The `-a` option will automatically generate a list of all repositories located in the directory.

### Examples

Pull a single repository:
```
./pull markqvist/Reticulum
```

Pull a list of repositories from a file:
```
./pull -f git_repos.list
```

Pull all repositories quietly:
```
./pull -a -q
```

See the full help text for the script:
```
./pull -h
```

## Dependencies

- git
- jq

Dependencies are easily installed on a Debian-based system:
```
apt install git jq
```
