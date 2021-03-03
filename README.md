# HandsOn Fullstack Clojure

_Closing the feedback loop for learning project scale Clojure(script)_

## Motivation

Clojure(script) is a modern Lisp dialect, and is a nice programming language in general. One philosophy that it has been consistently promoting is the [benefit of having a tight feedback loop](http://worrydream.com/LearnableProgramming/), and [REPL-driven development](https://dev.to/jr0cket/repl-driven-development-ano) is a prized gem (especially the state of hot reload in clojurescript).

Unfortunately, learning Clojure(script) has always have an impression of being a constant uphill battle _looking from the mainstream_ (whether this critique is fair/accurate or not is not the matter here - impression do matters.) In between the arcane syntax (most mainstream programming languages are descendent of C from a linguistic point of view, which is a distinct "evolutionary" branch from Lisp) and the complex tooling (Clojure(script) is in a sense a second layer language: Clojure layers on top of Java, while Clojurescript layers on top of Javascript), there is, in my opinion, a third factor that is sometimes overlooked: the **resource requirement to run a development environment**. This is what I hope to address here.

### What does it takes to see the REPL?

Clojure(script) processes are java program _hydrated_ with an embedded clojure interpreter. Running a JVM typically costs 1GB RAM per process for reasonable performance. With a modern setup with Clojurescript, using shadow-cljs, I believe you would need _at least 2_ separate JVM running. While there is a justification for being memory hungry (Java in the server world optimizes for performance _at scale_: as you scales up, how much "performance" can you deliver per GB RAM), this has the accidental side effect that **free cloud-based learning resources** that are generally available to other programming language is completely out of the question for Clojure(script). For example, the free tier of [REPL.it](https://repl.it/) offers container with 512MB memory (which is typical of free service). This is enough to run other mainstream languages (Python, NodeJS, and Go, in particular). With PaaS Hosting, the free tier overwhemlingly ranges from 512MB to 1GB. Thus while one _might_ be able to squeeze in a backend Clojure app, interactive frontend development (which is where the hot reload gem is) is still out of reach on the cloud.

### A Domino Effect

The _three factors_ I mentioned above are not independent, but interlocking, especially for beginners. The arcane syntax problem can, and indeed has been, overcome to a large extent thanks to the effort of many people writing **core language tutorials**. Once this initial phase of learning has completed successfully, however, one hit a kind of a brick wall:

- The transition from writing small, independent programs using just the core language, into proper Software Engineering that involves project management (not the business one) and the complex toolings mentioned above, represent a paradigm shift. While it may be feasible to [code-by-thinking](https://convincedcoder.com/2019/03/30/Hammock-driven-development/) all the way before, working with Software Project is fundamentally an empirical discipline, and thus _access to a live enviornment is not negotiable_.
- A beginner need to practise freely in such a live enviornment to learn this new paradigm. However, setting up such an enviornment presents a sort of a chicken-and-egg problem: one need to be minimally proficient at tooling, in order to setup the enviornment, in order to learn tooling!
- Traditionally, this problem can be solved by using a cloud based learning sandbox/lab/handson (whatever you call it). The principles are the same: break the gridlock by providing one enviornment that already has the tooling pre-installed, so that beginner can just dive in and experiment. Even better, these lab are often designed so that _mutations are not persisted after the session_. This helps a lot to assuage beginner's anxiety and fear of botching up an OS, which inhibits their boldness in using the computer.

Therefore, the heavy resource requirement of Clojure(script) ruled out free cloud based sandbox/labs, which, absent other methods to circumvent the chicken-and-egg problem, results in a prohibitively high barrier to transition into doing actual Software Project using Clojure(script). Which is a pity, as the benefit of REPL-driven development shines the brightest in the context of a full Software Project!

### Opportunistic leverage

Having said all these, all hopes are not lost. Cloud based development enviornment is not a new idea (e.g. Cloud9, which had a free tier before being absorbed into AWS). But there has been more activities on this front this few years: For the hyperscale cloud, Google Cloud Shell has been improving their offering, while Microsoft's Github Codespace is in limited preview. (Most major IaaS cloud vendor do have a cloud shell service now) Other vendors include gitpod (kind of a predecessor to codespace), and on the kubernetes local development front, okteto.

The last update to Google Cloud Shell [significantly extended](https://github.com/hkitsmallpotato/HandsOn_DevOps_Cloud#motivation) the scope of its potential/possibilities. This caught my attention, as 8GB RAM + `sudo` access means that it is finally practical to have a complete Clojure(script) development enviornment on it. By having a series of tutorials that are tightly integrated with the platform, it might just be possible to have the same, smooth on-ramping experience on both the learning (interactive tutorial) and the coding (REPL in a real enviornment) side. And by offering it on a cloud enviornment, it might just be possible to change the perception by lowering the perceived costs of learning.

## Usage

- For using it on Google Cloud Shell, follow the first few tutorials to setup the enviornment, then open VSCode in the browser, and open the coding tutorials inside VSCode.
- Alternatively, it is possible to use it on Gitpod by skipping the beginning tutorials. However in that case, one should use a docker image that has all Clojure(script) dev tools installed.
- Finally, since VSCode can run on almost any server, one can also deploy it (and the toolings) on any machine they can get their hands on (legally, of course). The tutorial favors installation methods that are completely user-space for this reason.

(Hint: To further assuage any anxiety, one can choose **not** to trust the repo when opening tutorials in Google Cloud Shell. This will results in Google allocating a _completely ephemeral_ VM to you, where even the home directory is mostly empty (and will be cleared after session ends). Of course your original home directory is actually still stored safely, tucked away from the current VM.)

(Hint: The last hint can be taken even further: as Google git clone the repo, you may do consecutive tutorials within the same completely ephemeral enviornment, simply by changing directory, then entering this command into the console: `teachme tutorial.md`)

## Content

Note that for Status:

- WIP means that it is still work in prgress
- Beta means it should be usable, but may lack polish
- Ready means it is ready for use.

| Lab                                             | Status    | Link                      |
|-------------------------------------------------|-----------|---------------------------|
| Installing VSCode (Code Server)                 | Beta      | [![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fhkitsmallpotato%2FHandsOn_Fullstack_Clojure.git&cloudshell_tutorial=install_vscode_codeserver%2Ftutorial.md&shellonly=true) |
| Install Didact VSCode Extension                 | Beta      | [![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fhkitsmallpotato%2FHandsOn_Fullstack_Clojure.git&cloudshell_tutorial=install_didact_vscode_extension%2Ftutorial.md) |
| Install Clojure and Clojurescript with Toolings | Beta      | [![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fhkitsmallpotato%2FHandsOn_Fullstack_Clojure.git&cloudshell_tutorial=install_clojure_clojurescript_toolings%2Ftutorial.md&shellonly=true) |
