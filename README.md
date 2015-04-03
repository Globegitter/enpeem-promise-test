# enpeem-promise-test

 - This test is based on PR https://github.com/balderdashy/enpeem/pull/4
 - As seen here: https://github.com/Globegitter/enpeem/blob/skip-dry-run-prefix-features/tests/runner.js#L9 I am using babeljs to transpile and polyfill my code only within the `tests` folder.
 - Checking the latest travis build: https://travis-ci.org/balderdashy/enpeem/builds/56950662 one can see that tests are passing fine on 0.10.x
 - Now running the code on Node 0.10.x in a non-test environment (via `node index.js`) one will see the following error (or similar):
 g
 ```js
 test-project/lib/index.js:4
var promise = new Promise(function (resolve, reject) {
                  ^
ReferenceError: Promise is not defined
    at Object.<anonymous> (test-project/lib/index.js:4:19)
    at Module._compile (module.js:456:26)
    at Object.Module._extensions..js (module.js:474:10)
    at Module.load (module.js:356:32)
    at Function.Module._load (module.js:312:12)
    at Module.require (module.js:364:17)
    at require (module.js:380:17)
    at Object.<anonymous> (test-project/tests/index.js:2:1)
    at Module._compile (module.js:456:26)
    at Object.Module._extensions..js (module.js:474:10)
```

- The problem now is even though the module does not actually work on node 0.10.x the tests make it seem the code actually is working, because the polyfills are leaking outside the specified `tests` folder.
