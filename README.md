# clojure-starter

Quick reference to setting up an awesome clojure dev environment.

## Steps

### 1. Required reading.
- http://dev.solita.fi/2014/03/18/pimp-my-repl.html
- https://github.com/zcaudate/vinyasa#installation
- http://thinkrelevance.com/blog/2013/06/04/clojure-workflow-reloaded

### 2. Set up ~/.lein/project.
```clojure
{:user {:plugins [[cider/cider-nrepl "0.7.0-SNAPSHOT"]]
        :dependencies [[spyscope "0.1.4"]
                       [org.clojure/tools.namespace  "0.2.6"]
                       [leiningen #=(leiningen.core.main/leiningen-version)]
                       [io.aviso/pretty "0.1.12"]
                       [org.clojars.gjahad/debug-repl "0.3.3"]
                       [difform "1.1.2"]
                       [im.chit/vinyasa "0.2.2"]]
        :injections
        [(require 'spyscope.core)
         (require '[vinyasa.inject :as inject])
         (require 'io.aviso.repl)
         (require 'com.georgejahad.difform)
         (require 'alex-and-georges.debug-repl)
         (inject/in ;; the default injected namespace is `.`

                    ;; note that `:refer, :all and :exclude can be used
                    [vinyasa.inject :refer [inject [in inject-in]]]
                    [vinyasa.lein :exclude [*project*]]

                    ;; imports all functions in vinyasa.pull
                    [vinyasa.pull :all]

                    ;; same as [cemerick.pomegranate
                    ;;           :refer [add-classpath get-classpath resources]]
                    [cemerick.pomegranate add-classpath get-classpath resources]

                    ;; inject into clojure.core with prefix
                    clojure.core >
                    [clojure.pprint pprint]
                    [alex-and-georges.debug-repl debug-repl]
                    [clojure.tools.namespace.repl [refresh refresh]]
                    [clojure.repl apropos dir doc find-doc source [root-cause cause]]
                    [com.georgejahad.difform difform]
                    [clojure.java.shell sh])]}}
```

### 3. Set up ./project.clj
```clojure
  (defproject clojure-starter "0.1.0-SNAPSHOT"
    :url "https://github.com/dqdinh/clojure-starter"
    :license {:name "MIT"}
    :dependencies [[org.clojure/clojure "1.6.0"]]
    :profiles {:dev {:dependencies [[org.clojure/tools.trace  "0.7.8"]]
                     :source-paths ["dev"]}})
```

### 4. Set up ./dev/user.clj
```clojure
  (ns user
    "Tools for interactive development with the REPL. This file should
    not be included in a production build of the application."
    (:require
     [clojure.tools.trace  :refer :all]
     ;; Add files you want to load in the repl here.
     ;; For example: [clojure-starter.vampires :refer :all].
     ;; Then in the repl, run (refresh).
     ))
```

### 5. workflow
- create new file / make updates to existing file
- in REPL, run (refresh)

## Useful Shortcuts
- lein install
- lein deps
- lein repl
