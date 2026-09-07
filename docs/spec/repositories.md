<!-- doc-id: repositories -->
# Repository contract

[한국어](repositories.ko.md)

<a id="ownership"></a>
## Ownership

The common repository owns the JSON specification, official inputs and expected results, shared verifier, implementation registry, and aggregate verification records. Each implementation repository owns its source, adapter, package metadata, documentation, and release process.

| Repository | Checkout path | Implementation |
| --- | --- | --- |
| ordered-json/ordered-json | . | Common contract and verification |
| ordered-json/javascript | js | JavaScript |
| ordered-json/rust | rust | Rust |
| ordered-json/go | go | Go |
| ordered-json/php | php | Pure PHP and the PHP Value API |
| ordered-json/php-extension | php-extension | Native PHP extension |

The common repository records exact implementation commits as Git submodules. Implementation repositories do not contain reverse submodules to the common repository. Pure PHP and the extension have separate source and release histories. The native implementation is tested with an explicitly selected PHP Value API revision.

<a id="verification"></a>
## Shared verification

Official inputs and expected results exist only in the common repository. Adapters return the shared reporting protocol and contain no independent goldens. The implementation registry declares repository locations, adapter commands, build commands, and runtime version commands. Adding a language must not require changing the JSON comparison algorithm.

A standalone implementation check fetches the common verifier at the full commit recorded in its conformance configuration and tests the current local implementation checkout. Required test dependencies also use full commit IDs. An explicit local verifier override is available for coordinated development. Test reports identify verifier sources, implementation sources, dependency revisions, runtimes, and results.

The aggregate check verifies every registered implementation using the checked-out submodule commits. It rejects missing or modified pinned submodules when recording an aggregate result. An implementation PR must run the shared check against its candidate source; the aggregate result applies only to the recorded combination.

<a id="documents"></a>
## Documents and changes

Each repository registers its own English documents and Korean translations. Shared contracts and aggregate feature state are referenced from implementation documents. The common documentation check also checks documents in initialized implementation repositories.

For a shared contract change, publish the verifier revision, update affected implementations and their conformance revision, run candidate checks, then update the common repository's submodule commits and run the aggregate check. Test success and source or package publication remain separate observations.

<a id="php-extension"></a>
## PHP extension package

The PHP library uses Composer package `ordered-json/ordered-json`. The extension uses the distinct PIE package `ordered-json/ordered-json-extension`, type `php-ext`, extension name `ordered_json`, and build path `src`. Its configuration enables a standalone extension build by default. The PHP library is a test dependency, not a native build or PIE package dependency.

PIE package validation and a local PIE build must succeed before recording PIE compatibility. A local build does not establish Packagist publication, a released version, Windows binary availability, or installation into a user's PHP configuration. The [PIE maintainer contract](https://github.com/php/pie/blob/1.5.x/docs/extension-maintainers.md) defines package metadata and build behavior.

<a id="state"></a>
## Implementation state

Repository separation is in progress. [Feature state](../features.md) records completion and evidence separately from this contract.
