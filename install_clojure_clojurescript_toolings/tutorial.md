# Install Clojure and Clojurescript with Toolings
  
## Overview

In this tutorial, you will setup your enviornment for Clojure and Clojurescript development by installing their toolings.

**Time needed**: Around 10 - 20 minutes (depending on the amount of customizations)

**Difficulty**: Easy

## Sketch of Roadmap

TODO

- Starting from Clojure 1.9, an [official command line client](https://clojure.org/guides/getting_started) system is introduced. (The usage guide is [here](https://clojure.org/guides/deps_and_cli))

## Install sdkman for Java version management

### Background

After Oracle's change of Java policy, there are many Java distributions. This [post](https://stackoverflow.com/questions/52431764/difference-between-openjdk-and-adoptium-adoptopenjdk) summarizes the situation.

We will use [sdkman](https://sdkman.io/) to manage Java versions. Be sure to read through each of its pages/documentation. Later we will use the command `sdk list java` to see a lists of available versions. The most relevant ones to us are:

- AdoptOpenJDK is the dominant open source option. The sub-versions are:
  - Hotspot (hs)
  - Eclipse OpenJ9 (j9)
  - [Upstream](https://adoptopenjdk.net/upstream.html) (open)
- Graalvm
- Java.net (i.e. [Oracle OpenJDK](http://jdk.java.net)) is Oracle's build of OpenJDK

As for the version number:

- Version 8 is the newest-old stable version. It has been there for a long time before, and is still in use by many legacy applications.
- Version 11 is the modern LTS (Long Term Support) version. It has accumulated [new platform and language features](https://dzone.com/articles/a-quick-catch-up-before-java-11), such as the module system, G1 garbage collector, as well as futher refining functional programming facilities first introduced in Java 8.
- Version 15 is the latest version.

### Installation

Note: Check whether it is already installed first by typing `sdk` into the command line.

Type the following into the terminal:

```bash
export SDKMAN_DIR="$HOME/.sdkman" && curl -s "https://get.sdkman.io" | bash
```

(We specified a custom location inside the home directory, so that it persists in Google Cloud Shell.)

You should see the following output (omiting the logo):

```
Looking for a previous installation of SDKMAN...
Looking for unzip...
Looking for zip...
Looking for curl...
Looking for sed...
Installing SDKMAN scripts...
Create distribution directories...
Getting available candidates...
Prime the config file...
Download script archive...
######################################################################## 100.0%
Extract script archive...
Install scripts...
Install contributed software...
renamed '/home/{user name}/.sdkman/tmp/stage/contrib/completion' -> '/home/{user name}/.sdkman/contrib/completion'
Set version to 5.11.0+644 ...
Attempt update of interactive bash profile on regular UNIX...
Attempt update of zsh profile...



All done!


Please open a new terminal, or run the following in the existing one:

    source "/home/{user name}/.sdkman/bin/sdkman-init.sh"

Then issue the following command:

    sdk help

Enjoy!!!
```

Then run

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Check the version

```bash
sdk version
```

```
==== BROADCAST =================================================================
* 2021-03-02: micronaut 2.3.4 available on SDKMAN!
* 2021-03-01: gradleprofiler 0.16.0 available on SDKMAN!
* 2021-03-01: gradleprofiler 0.15.5 available on SDKMAN!
================================================================================

SDKMAN 5.11.0+644
```

## Setting up Java

Get a list of available JVMs:

```bash
sdk list java
```

```
================================================================================
Available Java Versions
================================================================================
 Vendor        | Use | Version      | Dist    | Status     | Identifier
--------------------------------------------------------------------------------
 AdoptOpenJDK  |     | 15.0.2.j9    | adpt    |            | 15.0.2.j9-adpt
               |     | 15.0.2.hs    | adpt    |            | 15.0.2.hs-adpt
               |     | 11.0.10.j9   | adpt    |            | 11.0.10.j9-adpt
               |     | 11.0.10.hs   | adpt    |            | 11.0.10.hs-adpt
               |     | 11.0.9.open  | adpt    |            | 11.0.9.open-adpt
               |     | 8.0.282.j9   | adpt    |            | 8.0.282.j9-adpt
               |     | 8.0.282.hs   | adpt    |            | 8.0.282.hs-adpt
               |     | 8.0.275.open | adpt    |            | 8.0.275.open-adpt
 Alibaba       |     | 11.0.9.4     | albba   |            | 11.0.9.4-albba
               |     | 11.0.8       | albba   |            | 11.0.8-albba
...(snipped)...
 GraalVM       |     | 21.0.0.2.r11 | grl     |            | 21.0.0.2.r11-grl
               |     | 21.0.0.2.r8  | grl     |            | 21.0.0.2.r8-grl
               |     | 20.3.1.2.r11 | grl     |            | 20.3.1.2.r11-grl
               |     | 20.3.1.2.r8  | grl     |            | 20.3.1.2.r8-grl
               |     | 19.3.5.r11   | grl     |            | 19.3.5.r11-grl
               |     | 19.3.5.r8    | grl     |            | 19.3.5.r8-grl
 Java.net      |     | 17.ea.11     | open    |            | 17.ea.11-open
               |     | 17.ea.10     | open    |            | 17.ea.10-open
               |     | 17.ea.9      | open    |            | 17.ea.9-open
               |     | 17.ea.2.pma  | open    |            | 17.ea.2.pma-open
               |     | 17.ea.2.lm   | open    |            | 17.ea.2.lm-open
...(snipped)...
================================================================================
Use the Identifier for installation:

    $ sdk install java 11.0.3.hs-adpt
================================================================================
```

### Choosing a version


For our case, below is the recommended version (type `Y` if asked whether to make it the default):
```bash
sdk install java 11.0.10.hs-adpt
```

```
Downloading: java 11.0.10.hs-adpt

In progress...

########################################################################################################################################################################################## 100.0%########################################################################################################################################################################################## 100.0%

Repackaging Java 11.0.10.hs-adpt...

Done repackaging...

Installing: java 11.0.10.hs-adpt
Done installing!

Do you want java 11.0.10.hs-adpt to be set as default? (Y/n): Y

Setting java 11.0.10.hs-adpt as default.
```

### Confirmation

Verify that we have the correct version installed and activated in our enviornment:

```bash
sdk current java
```

```
Using java version 11.0.10.hs-adpt
```

```bash
java -version
```

```
openjdk version "11.0.10" 2021-01-19
OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.10+9)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.10+9, mixed mode)
```

Type this again:

```bash
sdk list java
```

You see something similar to:

```
================================================================================
Available Java Versions
================================================================================
 Vendor        | Use | Version      | Dist    | Status     | Identifier
--------------------------------------------------------------------------------
 AdoptOpenJDK  |     | 15.0.2.j9    | adpt    |            | 15.0.2.j9-adpt
               |     | 15.0.2.hs    | adpt    |            | 15.0.2.hs-adpt
               |     | 11.0.10.j9   | adpt    |            | 11.0.10.j9-adpt
               | >>> | 11.0.10.hs   | adpt    | installed  | 11.0.10.hs-adpt
               |     | 11.0.9.open  | adpt    |            | 11.0.9.open-adpt
               |     | 8.0.282.j9   | adpt    |            | 8.0.282.j9-adpt
               |     | 8.0.282.hs   | adpt    |            | 8.0.282.hs-adpt
               |     | 8.0.275.open | adpt    | installed  | 8.0.275.open-adpt
...(snipped)
```


## Install Leiningen

`lein` is the most used package manager for Clojure and its installation should be a pirority. Luckily, with sdkman, doing so is almost trivial. Just type:

```bash
sdk install leiningen
```

After it is done, verify that it is accessible from the command line:

```bash
lein -v
```

```
Leiningen 2.9.5 on Java 11.0.10 OpenJDK 64-Bit Server VM
```

## Install Boot

Again we want to customize the installation location to be inside the home directory. One good choice, aside from a dedicated hidden folder, is to use `~/bin`, which is considered to be the userland equivalent of `/usr/local/bin` by convention.

Remember to create the folder if it doesn't exists.

**After confirming the folder exists**, run the following one-liner to download the shim script:

```bash
sudo bash -c "cd $HOME/bin && curl -fsSLo boot https://github.com/boot-clj/boot-bin/releases/download/latest/boot.sh && chmod 755 boot"
```

Check that it is in `$PATH`:

```bash
echo $PATH
```

If it is not there, you can add it manually:

```bash
export PATH="$HOME/bin:$PATH"
```

Then type in `boot` to bootstrap its installation. You should see like:

```
Downloading https://github.com/boot-clj/boot/releases/download/2.7.2/boot.jar...
Running for the first time, BOOT_VERSION not set: updating to latest.
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by dynapath.defaults$fn__1516$fn__1517 (file:/home/xxx/.boot/cache/lib/2.7.2/aether.uber.jar) to method java.net.URLClassLoader.addURL(java.net.URL)
WARNING: Please consider reporting this to the maintainers of dynapath.defaults$fn__1516$fn__1517
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Retrieving clojure-1.8.0.pom from https://repo1.maven.org/maven2/ (8k)
Retrieving oss-parent-7.pom from https://repo1.maven.org/maven2/ (5k)
Retrieving maven-metadata.xml from https://repo.clojars.org/ (3k)
Retrieving boot-2.8.3.pom from https://repo.clojars.org/ (2k)
Retrieving boot-2.8.3.jar from https://repo.clojars.org/ (2k)
Retrieving clojure-1.8.0.jar from https://repo1.maven.org/maven2/ (3538k)
#http://boot-clj.com
#Wed Mar 03 07:08:31 UTC 2021
BOOT_VERSION=2.8.3
BOOT_CLOJURE_VERSION=1.8.0
BOOT_CLOJURE_NAME=org.clojure/clojure
```

Consider running `boot` **again** - it may auto-update itself for a second time.

Finally, check its version:

```bash
boot -V
```

```
#http://boot-clj.com
#Wed Mar 03 07:15:19 UTC 2021
BOOT_VERSION=2.8.3
BOOT_CLOJURE_VERSION=1.8.0
BOOT_CLOJURE_NAME=org.clojure/clojure
```

## Install Clojure command line

First, install its prerequisite. The most likely missing one is `rlwrap`:

```bash
sudo apt-get update
```

```bash
sudo apt-get install rlwrap
```

```
********************************************************************************
You are running apt-get inside of Cloud Shell. Note that your Cloud Shell
machine is ephemeral and no system-wide change will persist beyond session end.

To suppress this warning, create an empty ~/.cloudshell/no-apt-get-warning file.
The command will automatically proceed in 5 seconds or on any key.

Visit https://cloud.google.com/shell/help for more information.
********************************************************************************
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  rlwrap
0 upgraded, 1 newly installed, 0 to remove and 36 not upgraded.
Need to get 98.4 kB of archives.
After this operation, 296 kB of additional disk space will be used.
Get:1 http://deb.debian.org/debian buster/main amd64 rlwrap amd64 0.43-1+b1 [98.4 kB]
Fetched 98.4 kB in 0s (1,491 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package rlwrap.
(Reading database ... 115254 files and directories currently installed.)
Preparing to unpack .../rlwrap_0.43-1+b1_amd64.deb ...
Unpacking rlwrap (0.43-1+b1) ...
Setting up rlwrap (0.43-1+b1) ...
update-alternatives: using /usr/bin/rlwrap to provide /usr/bin/readline-editor (readline-editor) in auto mode
Processing triggers for man-db (2.8.5-2) ...
```

Create the installation directory manually by running `mkdir .clj-cli` in your home directory.

Then, download and run the install script:

```bash
curl -O https://download.clojure.org/install/linux-install-1.10.2.796.sh
```

```bash
chmod +x linux-install-1.10.2.796.sh
```

```bash
sudo ./linux-install-1.10.2.796.sh --prefix $HOME/.clj-cli
```

Output:

```
Downloading and expanding tar
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 16.7M  100 16.7M    0     0  71.8M      0 --:--:-- --:--:-- --:--:-- 71.8M
Installing libs into /home/xxx/.clj-cli/lib/clojure
Installing clojure and clj into /home/xxx/.clj-cli/bin
Installing man pages into /home/xxx/.clj-cli/share/man/man1
Removing download
Use clj -h for help.
```

Remember to add to the `$PATH` manually:

```bash
export PATH="$HOME/.clj-cli/bin:$PATH"
```

Verify its version:

```bash
clj --version
```

```
Clojure CLI version 1.10.2.796
```


## Install shadow-cljs

### Some technicalities


### Setup using node js project

Let's try it out. Create a dummy project:

```bash
npx create-cljs-project my-project
```

```
Need to install the following packages:
  create-cljs-project
Ok to proceed? (y) y
shadow-cljs - creating project: /home/xxx/my-project
Creating: /home/xxx/my-project/package.json
Creating: /home/xxx/my-project/shadow-cljs.edn
Creating: /home/xxx/my-project/.gitignore
Creating: /home/xxx/my-project/src/main
Creating: /home/xxx/my-project/src/test
----
Installing shadow-cljs in project.


added 96 packages, and audited 97 packages in 8s

3 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
----
Done. Actual project initialization will follow soon.
----
```

**Inside the project directory**, run:

```bash
npx shadow-cljs
```

```
shadow-cljs - config: /home/xxx/my-project/shadow-cljs.edn
shadow-cljs - updating dependencies
Retrieving thheller/shadow-cljs/2.11.19/shadow-cljs-2.11.19.pom from https://repo.clojars.org/
Retrieving org/clojure/clojure/1.10.1/clojure-1.10.1.pom from https://repo1.maven.org/maven2/
Retrieving org/clojure/data.json/1.0.0/data.json-1.0.0.pom from https://repo1.maven.org/maven2/
...(snipped)...
shadow-cljs - dependencies updated

Please specify which action to run!

Usage:
  shadow-cljs <action> <zero or more build ids>

Supported actions are:

     compile - ...
       watch - ...
       check - ...
...(snipped)
```

You can ask it to give versioning info:

```bash
npx shadow-cljs --cli-info
```

```
shadow-cljs - config: /home/xxx/my-project/shadow-cljs.edn
=== Version
jar:            2.11.19
cli:            2.11.19
deps:           1.3.2
config-version: 2.11.19

=== Paths
cli:     /home/xxx/my-project/node_modules/shadow-cljs/cli/dist.js
config:  /home/xxx/my-project/shadow-cljs.edn
project: /home/xxx/my-project
cache:   .shadow-cljs

=== Java
openjdk version "11.0.10" 2021-01-19
OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.10+9)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.10+9, mixed mode)

=== Source Paths
/home/xxx/my-project/src/dev
/home/xxx/my-project/src/main
/home/xxx/my-project/src/test

=== Dependencies
[thheller/shadow-cljs "2.11.19" :classifier "aot"]
...(snipped)
```

### Global install

Simply type:

```bash
npm install -g shadow-cljs
```

Afterwards, check that you can invoke the following **outside of any project directory**:

```bash
shadow-cljs --cli-info
```

Notice the path output - it should resides in a global location.

```
------------------------------------------------------------------------------

   WARNING: shadow-cljs not installed in project.
   See https://shadow-cljs.github.io/docs/UsersGuide.html#project-install

------------------------------------------------------------------------------
...(snipped)...
=== Paths
cli:     /usr/local/nvm/versions/node/v12.14.1/lib/node_modules/shadow-cljs/cli/dist.js
...(snipped)
```


## Congratulations!
