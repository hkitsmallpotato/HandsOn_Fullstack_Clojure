# Install Didact VSCode Extension

*Note*: This is a special tutorial that you may or may not need to use. Read this and the next page to determine if you need it.

## Overview

In this tutorial, you will install the [Didact](https://github.com/redhat-developer/vscode-didact) VSCode extension manually, by building from source.

**Time needed**: Around 10 minutes

**Difficulty**: Intermediate

## Situation

Normally, one can install extension from the VSCode UI. Even without the Microsoft Marketplace, one may use the [Open VSX Registry](https://open-vsx.org/) as a substitute. However, due to the unstable and rapidly evolving state of the `didact` extension, the situation as of 1st March, 2021 is embarassing:

- The latest version of `code-server` is 3.9.0, which comes with VSCode version 1.52.1 only.
- The latest release of `didact` is v0.3.1, which is set to _requires_ at least VSCode v1.53.0.
  - Attempting to install it anyway will results in an error message stating that the extension is incompatible.
- The previous release of `didact` is v0.3.0. It only requires VSCode v1.52.0.
  - However, it has a critical bug that renders it completely unusable as it cannot even starts (v0.3.1 is an urgent bugfix of that)
- There are older versions of `didact` that should work. Unluckily, the recentish version only have source distribution.
  - The most recent binary release, other than the above, is 0.1.18, which is 4 months old.

Therefore, the only practical way to proceed today, would be to manually build the extension from source using a recent version, while fixing the problem ourselves.

## Checking out and patching the source

Check out the source repository:

```bash
git clone https://github.com/redhat-developer/vscode-didact.git && cd vscode-didact/
```

Then checkout the most recent tag:

```bash
git checkout tags/0.3.1
```

(Note: this results in a detached HEAD state. Exercise caution for some operations.)

We have prepared a patch. The extension actually do work on VSCode 1.52.0, so we just need to change the package file's indication of which version is accepted.

Look at the change before applying patch:

```bash
cat ~/cloudshell_open/HandsOn_Fullstack_Clojure/install_didact_vscode_extension/didact_vscode_ver_patch.patch
```

```bash
git apply ~/cloudshell_open/HandsOn_Fullstack_Clojure/install_didact_vscode_extension/didact_vscode_ver_patch.patch
```

Confirm that the changes are applied:

```bash
git diff
```

## Building the extension

The CI file contains instruction on how to build from source. In this case it is `JenkinsFile`. We simply copy it:

```bash
npm install -g typescript vsce
```

```bash
npm ci
```

```bash
npm run vscode:prepublish
```

```bash
vsce package -o vscode-didact-custom.vsix
```

Take note of the location where the extension file is.

(Hint: you can see your current directory's full path by the command `pwd`.)

## Install extension from .vsix file

1. Open the VSCode UI in your web browser.
2. Click the extension button.
3. Click the top right hand corner of the panel, then click "Install from .vsix..."
4. Select the `.vsix` files you built in the last step.
5. Restart VSCode by refreshing the webpage for the installed extension to take effect.

If you are successful, you should see a new Didact tutorial view on the left panel.

(Hint: The `didact` source repo itself contains some sample tutorials in the `demos/markdown` folder. They will show up in the panel once you click on that folder)

## Congratulations!

TODO
