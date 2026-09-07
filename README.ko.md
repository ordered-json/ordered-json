<!-- doc-id: overview -->
<!-- source-sha256: 2bf37ab0505b6248c3ddea187753d4068ce1c98c78f3ea9ee12ab04547b506db -->
# ordered-json

[English](README.md)

JavaScript, Rust, Go, PHP용 JSON 라이브러리입니다. 객체는 모든 깊이에서 문서 키 순서를 유지하는 연관배열을 사용합니다. 중복 키는 최초 위치와 마지막 값을 유지합니다.

이 저장소는 공통 명세, 공식 예제, 기대 결과, 검증기를 관리합니다. 독립된 구현 저장소 다섯 개를 정확한 커밋의 서브모듈로 포함합니다. PHP와 네이티브 PHP 확장은 별도 저장소입니다.

<a id="start"></a>
## 시작

~~~sh
git clone --recurse-submodules https://github.com/ordered-json/ordered-json.git
cd ordered-json
~~~

기존 체크아웃은 `git submodule update --init --recursive`를 실행합니다. 저장소 루트에서 공식 입력으로 JavaScript를 실행합니다.

~~~sh
node --input-type=module <<'JS'
import {readFileSync} from 'node:fs';
import {parse, stringify} from './js/index.js';
const {cases} = JSON.parse(readFileSync('examples/official.json', 'utf8'));
const example = cases.find(example => example.id === 'document-order');
console.log(stringify(parse(example.input)));
JS
~~~

| 저장소 | 내용 | 체크아웃 경로 |
| --- | --- | --- |
| [javascript](https://github.com/ordered-json/javascript) | JavaScript 및 TypeScript 선언 | `js/` |
| [rust](https://github.com/ordered-json/rust) | Rust | `rust/` |
| [go](https://github.com/ordered-json/go) | Go | `go/` |
| [php](https://github.com/ordered-json/php) | 순수 PHP 및 Value API | `php/` |
| [php-extension](https://github.com/ordered-json/php-extension) | PIE 메타데이터를 제공하는 네이티브 PHP 확장 | `php-extension/` |

<a id="verification"></a>
## 검증

모든 구현이 같은 [공식 예제](examples/README.ko.md)와 공통 기대값을 사용합니다. 각 구현 저장소도 현재 체크아웃을 검사하는 `make check`를 제공합니다.

~~~sh
make check
~~~

통합 기록은 고정된 서브모듈 커밋에 적용됩니다. 도구와 식별자는 [설치](docs/operations/installation.ko.md), 단독·추가 사례·PIE 검사는 [검증](docs/operations/validation.ko.md)을 참조합니다. 테스트와 패키지 게시는 별도로 기록합니다.

<a id="documents"></a>
## 문서

- [JSON 계약](docs/spec/json-contract.ko.md)
- [API 계약](docs/spec/api.ko.md)
- [저장소 계약](docs/spec/repositories.ko.md)
- [기능 상태](docs/features.ko.md)
- [배포 상태](docs/operations/distribution.ko.md)
- [변경 기록](CHANGELOG.ko.md)
- [문서 관리](docs/documentation-plan.ko.md)
- [개발 절차](AGENTS.ko.md)
- [요청된 비교 보고서](docs/reports/ojson-comparison.ko.md)
