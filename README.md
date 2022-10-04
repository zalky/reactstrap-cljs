<img src="https://i.imgur.com/GH71uSi.png" title="zalky" align="right" width="250"/>

# Reactstrap-cljs

[![Clojars Project](https://img.shields.io/clojars/v/io.zalky/reactstrap-cljs?labelColor=blue&color=green&style=flat-square&logo=clojure&logoColor=fff)](https://clojars.org/io.zalky/reactstrap-cljs)

A Clojurescript/Reagent adapter around [Reactstrap
9](https://github.com/reactstrap/reactstrap) and by extension
[Bootstrap 5](https://getbootstrap.com/).

## Usage

1. Include the adapter as a dependency in your `deps.edn`:

   ```clj
   {io.zalky/reactstrap-cljs {:mvn/version "0.1.0"}}
   ```

2. Bring in Reactstrap as an external
   dependency. [`shadow-cljs`](https://github.com/thheller/shadow-cljs)
   makes npm integration easy: just add Reactstrap to your
   `packages.json`.

3. You will also need to provide some version the Bootstrap 5 CSS. The
   simplest way is using a [CDN
   link](https://getbootstrap.com/docs/5.2/getting-started/download/#cdn-via-jsdelivr).

Once you have succesfully configured the above, you should be able to
require `reactstrap-cljs.core` and refer to all Reactstrap components
by their kebab-case equivalent:

```clj
(ns my.project
  (:require [reactstrap-cljs.core :as b]))

(defn sidebar-entry
  [_]
  [b/nav-item
   [b/nav-link {:href "/"}
    [util/icon "bell"]
    [:span "Notifications"]]])
```

## Bootstrap SASS

If instead of vanilla CSS you want to extend Bootstrap SASS, the
easiest way to include it is via the `org.webjars/bootstrap` webjar
and the [dart-sass-clj](https://github.com/zalky/dart-sass-clj)
embedded compiler:

```clj
{:sass {:extra-deps {io.zalky/dart-sass-clj {:mvn/version "0.2.0"}
                     org.webjars/bootstrap  {:mvn/version "5.2.2"}}
        :main-opts  ["-m" "dart-sass-clj.core"
                     "--source-dirs" "[\"src/my/scss\"]"
                     "--target-dir" "resources/assets/"
                     "--output-style" ":expanded"
                     "--source-maps"
                     "--watch"]}}
```

Then `@import` what you need according to the [semantics of webjar
import](https://github.com/zalky/dart-sass-clj#imports). For example:

```css
@import "bootstrap/scss/bootstrap";
@import "bootstrap/scss/bootstrap-grid";
@import "bootstrap/scss/bootstrap-reboot";
```

## License

Distributed under the terms of the Apache License 2.0.
