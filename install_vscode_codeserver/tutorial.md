# Installing VSCode (Code Server)

## Overview

In this tutorial, we will install the Code Server Version of VSCode.

**Prerequisite**: (Optional, if cloud proxy is used) A github account.

**Time needed**: About 5 minutes

**Difficulty**: Easy

## Background

TODO

### VSCode on Google Cloud Shell

Google Cloud Shell provide a Theia based IDE. It is good enough for many purpose, however, it is subject to the limitation that it does not support installing extension. One possible reason is that Microsoft has imposed a restriction prohibiting anyone else from using the official Microsoft VSCode Extension Marketplace.

If your workflow *requires* using extension, then installing `code-server` is a solution. It uses an [open source marketplace](https://open-vsx.org/) independent from Microsoft's one. You can also install extension directly from a `.vsix` file.

## Standalone install

The [official repo](https://github.com/cdr/code-server) has detailed documentation on how to install. Because the environment on which you want to run VSCode can be very diverse, including those where you only have normal user privilege without `sudo` or `root` access, the safest/most universal, "standalone" installation method is shown here.

Open a **new, unused** terminal, and run the following code:
```bash
curl -fsSL https://code-server.dev/install.sh | sh -s -- --method=standalone --prefix=/tmp/mycdr --dry-run
```

It will shows what commands will be run during a real install. The arguments' explanations are:

- `--method=standalone`: Use standalone installation method
- `--prefix=/tmp/mycdr`: Installation directory (default: `~/.local`)
- `--version=3.9.0`: Fix which version to use instead of the latest one
- `--dry-run`: Show commands only; don't run.

You may modify the command according to your preference. For example, in Google Cloud Shell, if you want the install to persist across session, either omit the `--prefix` argument, or choose one that is inside your home directory.

(Note: As of 1st March, 2021, The latest version of code server is 3.9.0, and it runs VSCode version 1.52.1 behind the scene.)

When you are ready, run your command again, ommiting the `--dry-run` argument. You should see an output like this:

```
Debian GNU/Linux 10 (buster)
Installing standalone release archive v3.9.0 from GitHub releases.

+ mkdir -p ~/.cache/code-server
+ curl -#fL -o ~/.cache/code-server/code-server-3.9.0-linux-amd64.tar.gz.incomplete -C - https://github.com/cdr/code-server/releases/download/v3.9.0/code-server-3.9.0-linux-amd64.tar.gz
########################################################################################################################################################################################## 100.0%########################################################################################################################################################################################## 100.0%
+ mv ~/.cache/code-server/code-server-3.9.0-linux-amd64.tar.gz.incomplete ~/.cache/code-server/code-server-3.9.0-linux-amd64.tar.gz
+ sudo mkdir -p /tmp/mycdr/lib /tmp/mycdr/bin
+ sudo tar -C /tmp/mycdr/lib -xzf ~/.cache/code-server/code-server-3.9.0-linux-amd64.tar.gz
+ sudo mv -f /tmp/mycdr/lib/code-server-3.9.0-linux-amd64 /tmp/mycdr/lib/code-server-3.9.0
+ sudo ln -fs /tmp/mycdr/lib/code-server-3.9.0/bin/code-server /tmp/mycdr/bin/code-server

Standalone release has been installed into /tmp/mycdr/lib/code-server-3.9.0
Please extend your path to use code-server:
  PATH="/tmp/mycdr/bin:$PATH"
Then you can run:
  code-server
```

Run the command as instructed by the output to update your `$PATH` enviornment variable:
```
PATH="{your install directory}:$PATH"
```

## Run code-server using Coder cloud proxy

`code-server` has recently added a feature to provide a cloud hosted, SaaS style proxy, as an alternative to configuring internet access, certificate, security, etc manually.

On the same console, simply run:
```bash
code-server --link
```

The output is similar to the following (sensitive info are masked):

```
[2021-03-01T12:22:00.773Z] info  Wrote default config file to ~/.config/code-server/config.yaml
[2021-03-01T12:22:01.269Z] info  code-server 3.9.0 fc6d123da59a4e5a675ac8e080f66e032ba01a1b
[2021-03-01T12:22:01.272Z] info  Using user-data-dir ~/.local/share/code-server
[2021-03-01T12:22:01.291Z] info  Using config file ~/.config/code-server/config.yaml
[2021-03-01T12:22:01.291Z] info  HTTP server listening on http://127.0.0.1:40695 (randomized by --link)
[2021-03-01T12:22:01.291Z] info    - Authentication is disabled (disabled by --link)
[2021-03-01T12:22:01.291Z] info    - Not serving HTTPS (disabled by --link)
[2021-03-01T12:22:01.554Z] info  Detected an acceptable latency of 17ms
[2021-03-01T12:22:01.969Z] info  visit https://github.com/login/oauth/authorize?client_id=xxx&response_type=code&scope=read%3Auser+user%3Aemail&state=xxx to login
[2021-03-01T12:22:32.713Z] info  Proxying code-server to Coder Cloud, you can access your IDE at https://somedomain.cdr.co
```

Remember to click on the github link - it will redirect you to your github account and ask for OAuth permission. Grant it, then wait.

## (Optional) Amend shell prompt in terminal in VSCode

If you are running it on Google Cloud Shell, you may notice that for terminals *inside* code server, the shell prompt has the word "cloudshell" suffixed, which interfere with viewing. (This case occur if you do not have an active GCP project selected)

To remedy this, you may manually change the `$PS1` variable:

```bash
echo $PS1 > ps1.txt
```

The content should look like this:

```
\[\e]0;${DEVSHELL_PROJECT_ID:-Cloud Shell}\a\]\u@cloudshell:\[\033[1;34m\]\w$([[ -n $DEVSHELL_PROJECT_ID ]] && printf " \[\033[1;33m\](%s)" ${DEVSHELL_PROJECT_ID} )\[\033[00m\]$ \[\033k$([[ -n $DEVSHELL_PROJECT_ID ]] && printf "(%s)" ${DEVSHELL_PROJECT_ID} || printf "cloudshell")\033\\\]
```

Edit the file, removing the `|| printf "cloudshell"` near the end, then save.

Update the enviornment variable:
```bash
export PS1=`cat ps1.txt`
```

## Congratulations!

TODO
