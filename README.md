# Rollcage
[![Circle CI](https://circleci.com/gh/nedap/rollcage.svg?style=svg)](https://circleci.com/gh/nedap/rollcage)

A Clojure client for [Rollbar](http://rollbar.com)

## Installation

Rollcage is available on [Clojars](https://clojars.org/nedap/rollcage).

### Leiningen/Boot

```clojure
[nedap/rollcage "1.0.0"]
```

### Clojure CLI/deps.edn

```clojure
nedap/rollcage {:mvn/version "1.0.0"}
```

## Quickstart

You can send exceptions like this:

```Clojure
user=> (require '[nedap.rollcage.core :as rollcage])

user=> (def r (rollcage/client "access-token" {:environment "staging"}))

user=> (try
  #_=>   (/ 0)
  #_=>   (catch Exception e
  #_=>     (rollcage/error r e)))
{:err 0, :result {:id nil, :uuid "420cfa6e-40d1-431d-80ef-575520c40dd7"}}
```

You can also setup handler for all UncaughtExceptions.
Call this fn during start-up procedure to ensure all uncaught exceptions
will be sent to Rollbar.

```clj
user=> (rollcage/setup-uncaught-exception-handler r)
```

## Contributing

If you would like to contibute to the project, please [log an issue](https://github.com/nedap/rollcage/issues) to discuss the feature/bug before submitting a pull request.

## Testing

A full CI suite is [run on CircleCI](https://circleci.com/gh/nedap/rollcage).
You can run the unit-test suite locally by running `lein test`. Some tests
require access to Rollbar, with a valid access token that has permission to post
server items. The token should be specified in the ROLLBAR_ACCESS_TOKEN
environment variable.

```bash
$ ROLLBAR_ACCESS_TOKEN=<your token> lein test
```

The tests that require access to Rollbar are annotated with the `:integration`
metadata tag. You can exclude these by using the `:unit` test selector.

```bash
$ lein test :unit
```


## Releasing

Releases are published [to Clojars under the Nedap organisation](https://clojars.org/nedap/rollcage).
You can release a new version of Rollcage by editing the version string in
`project.clj` according to [semver](http://semver.org/). Then run

```bash
$ git tag v<version>
$ git push --tags
```

## License

Distributed under the [Eclipse Public License](http://www.eclipse.org/legal/epl-v10.html).
