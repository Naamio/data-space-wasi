# Naamio Data Space WASI Specifications

The WebAssembly Interface Type (WIT) packages that define how
[Naamio Data Space](https://naamio.space) extensions talk to the host that runs them. A
package here is the contract between the extension host and every component written for
it, first-party or third-party, in any language that targets the WebAssembly component
model.

## Design

Naamio Data Space extends through WebAssembly components running on WebAssembly System
Interface (WASI) 0.3. A component knows one syntax, such as Turtle, and the host owns
meaning: anything more than one component would need lives in the host. A parser reads
bytes and streams back the statements a document makes, as written, and the host resolves
Internationalized Resource Identifiers (IRIs), expands prefixes, gives blank nodes their
identity, checks every term, and stores the result. Resource Description Framework (RDF)
data crosses the boundary as typed statements, never as text for the host to parse a
second time.

The `linked-data:rdf` package is not specific to Naamio. Its worlds import no functions,
only interfaces that declare types, so any host that runs WebAssembly components can run a
component written against them, and any library author can write one.

The contract is the same on every platform the host runs on, whether that is a long-running
daemon or an engine embedded in an application. Only how the host executes a component
differs.

Code repositories that build against these packages include this repository as a Git
submodule, so a host and its components always name the exact contract revision they
were built with.

## Background

The architectural background is recorded in the
[Naamio Data Space architecture repository](https://github.com/Naamio/data-space-architecture).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how changes to the contract are proposed and
what is checked before they land.

## Licence

MPL-2.0. Copyright (c) Omnifi Foundation.
