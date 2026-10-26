# Comment draft for the open issue https://github.com/hexlet-codebattle/battle_asserts/issues/1093

Still reproducible on production on 2026-10-26.

**Environment**
- Task data: GET https://codebattle.hexlet.io/api/v1/tasks/32 (`nrzi_encoding`, level easy, 30 asserts); the task now lives in https://github.com/hexlet-codebattle/tasks (`tasks/easy/strings/nrzi_encoding.toml`)
- Codebattle frontend build `bea05b21db2ee2a63311d6f9fc2faca8`, latest master commit 285744f (2026-10-23)
- Local run: g++ 14.2.0 (Debian, Docker), Node.js 22.19.0; OS Windows 11 Pro 10.0.22000

**Steps**
1. Take the 30 asserts of `nrzi_encoding` from the API above.
2. Solve it char by char: skip `|`, append `1` if the previous char is `|`, otherwise `0`.
3. Run the same solution in JavaScript and in C++ (`std::string`).

**Expected:** the same correct solution passes all 30 tests in both languages.

**Actual:** JavaScript passes 30/30, C++ passes 3/30. The inputs contain `¯` (U+00AF, 2 bytes in UTF-8), so `std::string` sees it as two chars. Example: `¯|___|¯¯¯¯¯|___|¯|_|¯` (21 chars, 29 bytes) → expected `010010000100111`, C++ returns `00100100000000010010110`.

Replacing `¯` with an ASCII character (for example `-`) in the task description and asserts would make the task fair for C++ (and other byte-oriented string languages).

Log: attach `assets/nrzi-encoding-non-ascii.txt` from https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85
