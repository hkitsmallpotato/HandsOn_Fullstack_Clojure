(DRAFT)

# Clojure Project Management via Lein

Reference: 
https://github.com/technomancy/leiningen/blob/master/doc/TUTORIAL.md

https://github.com/technomancy/leiningen/blob/master/sample.project.clj
(Contain many possible configuration parameters in `project.clj`)

https://gist.github.com/ghoseb/287710
Clojure ns syntax cheat-sheet

https://cognitect.com/blog/2013/06/04/clojure-workflow-reloaded
Manually creating a way to reload stuff in REPL

## Skaffold project by template

```bash
lein new app my-stuff
```

```
Generating a project called my-stuff based on the 'app' template.
```


## Dependency Management

Asks to add dependency to `project.clj`, then run:

```bash
lein deps
```

## REPL

Start a repl by `lein repl`:

```
nREPL server started on port 55568 on host 127.0.0.1 - nrepl://127.0.0.1:55568
REPL-y 0.4.4, nREPL 0.8.3
Clojure 1.10.1
OpenJDK 64-Bit Server VM 1.8.0_222-b10
    Docs: (doc function-name-here)
          (find-doc "part-of-name-here")
  Source: (source function-name-here)
 Javadoc: (javadoc java-object-or-class-here)
    Exit: Control+D or (exit) or (quit)
 Results: Stored in vars *1, *2, *3, an exception in *e

my-stuff.core=>
```

Type some command to see that it works.

Modify file, then reload.

Run the program from command line using `lein run`

## Options for compiling for production

Uberjar:

```bash
lein uberjar
```

```
Compiling my-stuff.core
Created /home/phil/my-stuff/target/uberjar+uberjar/my-stuff-0.1.0-SNAPSHOT.jar
Created /home/phil/my-stuff/target/uberjar/my-stuff-0.1.0-SNAPSHOT-standalone.jar
```

Uberjar can be run directly as java program, without the infamous JAR classpath hell:

```bash
java -jar my-stuff-0.1.0-SNAPSHOT-standalone.jar Hello world.
```

Normal jar:

`lein compile` then `lein jar`?

## Nrepl Server

To start server: `lein repl :headless`

To connect to a running nrepl server (on client side): `lein repl :connect <port>`

```
Connecting to nREPL at 127.0.0.1:57535
REPL-y 0.3.7, nREPL 0.2.12
```

## Profile and nrepl middlewares

https://github.com/technomancy/leiningen/blob/master/doc/PROFILES.md

Edit project.clj file, then use `with-profile` in lein option.

Allows isolating config that are context dependent.

Middleware in web programming can be extended to repl protocol too:

https://nrepl.org/nrepl/design/middleware.html

This one is what we need to support more IDE integration:

https://github.com/clojure-emacs/refactor-nrepl



## Connecting using Calva


