# Contributing to the Naamio Data Space WASI Specifications

Start with the [README](README.md) for what this repository is and who depends on it.

## The contract comes after the decision

A change to a package here changes what every host and every component must do. Propose it
first as a decision or comment in the
[architecture repository](https://github.com/Naamio/data-space-architecture), and link that
record from the merge request. A merge request that changes the contract without a record
is not reviewed until one exists.

## Versions

Every package carries a semantic version in its `package` declaration, for example
`package linked-data:rdf@0.0.0;`. While a package is below 1.0, any release may break
compatibility, and the record that motivates a break says so. From 1.0, a removal or a
changed signature is a major version, and an addition is a minor version.

A host and its components pin a revision of this repository as a Git submodule, so a new
version reaches them only when their own repository moves the submodule forward.

## Gates

Every package must parse and resolve both without and with its unstable features:

```shell
wasm-tools component wit <package-directory>
wasm-tools component wit --all-features <package-directory>
```

An interface still being designed is marked `@unstable(feature = <name>)`. The mark has to
appear on every item inside the interface as well, including its `use` statements, or the
first command fails. A host or component that implements an unstable interface opts in to
the feature by name.

A package that imports another package, here or from WASI, vendors it under that package's
`deps/` directory at the version it was written against.

## Names

Interfaces, types, functions and parameters are named for what they mean in the domain,
in kebab-case and without abbreviations: `configuration`, not `config`. `misc`, `common`,
`core`, `utils`, `shared` and `types` are refused as interface names, each one a place a
decision got deferred rather than made. "User" is refused too: name the person by their
role, such as *account holder*, *operator* or *developer*.

## Comments

Every interface, type, function and resource is documented with `///` comments: what it
does, what each argument means, what it returns, and when it fails. The documentation is
the specification. Someone implementing a host in another language reads these comments
and nothing else.

Write for someone reading English as an additional language, and for someone meeting the
contract for the first time. Say what something does and why it is that way.

Every `.wit` file carries an SPDX header:

```wit
// SPDX-FileCopyrightText: 2026 Omnifi Foundation
// SPDX-License-Identifier: MPL-2.0
```

## Commits and merge requests

Commit messages are a single line, in the imperative, specific enough to identify the
change. Detail belongs in the merge request.

Keep unrelated changes apart. A rename, a formatting pass, and a behaviour change are three
merge requests, because reviewing them together means reviewing none of them properly.
