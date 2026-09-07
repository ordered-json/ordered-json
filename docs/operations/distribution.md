<!-- doc-id: distribution -->
# Distribution

[한국어](distribution.ko.md)

<a id="state"></a>
## Observed state

[distribution.json](../distribution.json) records source and publication observations. The common repository and five [implementation repositories](../spec/repositories.md#ownership) have public `main` branches. Each implementation observation identifies the confirmed source commit. No GitHub releases or version tags were found in the recorded observations.

Registry publication for npm, crates.io, Packagist, Go, and the PHP extension is not verified. Source checkout is the confirmed distribution. PIE metadata and a passing [PIE build](../pie-verification.json) establish local build compatibility, not Packagist publication. The extension package is `ordered-json/ordered-json-extension`; the PHP library is `ordered-json/ordered-json`.

Source version strings do not establish a released artifact. Registry publishing workflows and hosted CI are not configured. LICENSE files are not present.

<a id="source-publication"></a>
## Source publication

Run each changed implementation's required checks, commit its source, and publish that implementation before updating the common submodule commit. For each authorized source push:

~~~sh
git push origin main
git rev-parse HEAD
git ls-remote origin refs/heads/main
~~~

Confirm that the full local and remote commit IDs match. Update the common checkout to those published commits, stage the submodule paths, run the aggregate and applicable PIE checks, then commit and publish the common change. Verify a recursive clone can fetch every pin. A shared contract change first requires publishing the verifier revision used by the implementation checks.

Keep authentication information in the system credential store or private memory. Keep publication observations separate from test results.

<a id="releases"></a>
## Registry and release records

No registry publication is established or verified. Before recording a release, verify its package name, version, included files, registry, artifact, and tested source revision. Record the artifact URL and publication observation separately. Register the extension for PIE through Packagist using its `php-ext` Composer metadata when publishing a release.

Update English and Korean distribution documents, feature distribution state, and the changelog when publication state changes. Do not infer publication from a test, version declaration, planned tag, or source push.
