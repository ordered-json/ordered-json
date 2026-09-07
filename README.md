<!-- doc-id: overview -->
# ordered-json

[한국어](README.ko.md)

JSON libraries for JavaScript, Rust, Go, and PHP. Objects use associative maps that preserve document key order at every depth. Repeated keys retain the first position and the last value.

This repository maintains the common specification, official examples, expected results, and verifier. Five independent implementation repositories are included as submodules at exact commits. PHP and the native PHP extension have separate repositories.

<a id="start"></a>
## Start

~~~sh
git clone --recurse-submodules https://github.com/ordered-json/ordered-json.git
cd ordered-json
~~~

For an existing checkout, run `git submodule update --init --recursive`. Run JavaScript with an official input from the repository root:

~~~sh
node --input-type=module <<'JS'
import {readFileSync} from 'node:fs';
import {parse, stringify} from './js/index.js';
const {cases} = JSON.parse(readFileSync('examples/official.json', 'utf8'));
const example = cases.find(example => example.id === 'document-order');
console.log(stringify(parse(example.input)));
JS
~~~

| Repository | Contents | Checkout path |
| --- | --- | --- |
| [javascript](https://github.com/ordered-json/javascript) | JavaScript and TypeScript declarations | `js/` |
| [rust](https://github.com/ordered-json/rust) | Rust | `rust/` |
| [go](https://github.com/ordered-json/go) | Go | `go/` |
| [php](https://github.com/ordered-json/php) | Pure PHP and the Value API | `php/` |
| [php-extension](https://github.com/ordered-json/php-extension) | Native PHP extension with PIE metadata | `php-extension/` |

<a id="verification"></a>
## Verification

All implementations use the same [official examples](examples/README.md) and shared expectations. Each implementation repository also provides `make check` for its current checkout.

~~~sh
make check
~~~

The aggregate record applies to the pinned submodule commits. See [installation](docs/operations/installation.md) for tools and identifiers, and [verification](docs/operations/validation.md) for standalone, supplementary, and PIE checks. Tests and package publication are recorded separately.

<a id="documents"></a>
## Documents

- [JSON contract](docs/spec/json-contract.md)
- [API contract](docs/spec/api.md)
- [Repository contract](docs/spec/repositories.md)
- [Feature state](docs/features.md)
- [Distribution state](docs/operations/distribution.md)
- [Changelog](CHANGELOG.md)
- [Documentation management](docs/documentation-plan.md)
- [Development procedure](AGENTS.md)
- [Requested comparison report](docs/reports/ojson-comparison.md)
