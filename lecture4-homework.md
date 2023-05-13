# 第4课 课后作业

## 第1题

```shell
[sintan1071]% npm i -g @semaphore-protocol/cli@latest
npm WARN deprecated @npmcli/move-file@2.0.1: This functionality has been moved to @npmcli/fs

added 352 packages in 10s
[MacBook-Pro-2:SuTu]
[sintan1071]% semaphore create my-app --template monorepo-ethers

 ✔ Your project is ready!

 Please, install your dependencies by running:

   cd my-app
   npm i

 Available scripts:

   npm run dev
   npm run dev:web-app
   npm run dev:contracts
   npm run lint
   npm run prettier
   npm run prettier:write
   npm run copy:contract-artifacts
   npm run prepublish

 See the README.md file to understand how to use them!

[sintan1071]% npm i
npm WARN deprecated mkdirp-promise@5.0.1: This package is broken and no longer maintained. 'mkdirp' itself supports promises now, please switch to that.
npm WARN deprecated request-promise-native@1.0.9: request-promise-native has been deprecated because it extends the now deprecated request package, see https://github.com/request/request/issues/3142
npm WARN deprecated rollup-plugin-terser@7.0.2: This package has been deprecated and is no longer maintained. Please use @rollup/plugin-terser
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
npm WARN deprecated fsevents@2.1.3: "Please update to latest v2.3 or v2.2"
npm WARN deprecated sourcemap-codec@1.4.8: Please use @jridgewell/sourcemap-codec instead
npm WARN deprecated debug@3.2.6: Debug versions >=3.2.0 <3.2.7 || >=4 <4.3.1 have a low-severity ReDos regression when used in a Node.js environment. It is recommended you upgrade to 3.2.7 or 4.3.1. (https://github.com/visionmedia/debug/issues/797)
npm WARN deprecated uuid@2.0.1: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated uuid@2.0.1: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated multicodec@1.0.4: This module has been superseded by the multiformats module
npm WARN deprecated uuid@3.4.0: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated uuid@3.3.2: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated multibase@0.6.1: This module has been superseded by the multiformats module
npm WARN deprecated multibase@0.7.0: This module has been superseded by the multiformats module
npm WARN deprecated multicodec@0.5.7: This module has been superseded by the multiformats module
npm WARN deprecated cids@0.7.5: This module has been superseded by the multiformats module
npm WARN deprecated snarkjs@0.4.13: Sucurity bug fixed

> @semaphore-protocol/cli-template-monorepo-ethers@3.9.0 prepublish
> tar -czf files.tgz .gitignore .yarn .yarnrc.yml apps


added 1563 packages in 1m

[sintan1071]% cd apps/contracts 
[MacBook-Pro-2:contracts]
[sintan1071]% ls
contracts         hardhat.config.ts package.json      scripts           tasks             test              tsconfig.json
[MacBook-Pro-2:contracts]
[sintan1071]% npm run compile      

> monorepo-ethers-contracts@1.0.0 compile
> hardhat compile

Downloading compiler 0.8.4
Generating typings for: 12 artifacts in dir: ./build/typechain for target: ethers-v5
Successfully generated 40 typings!
Compiled 14 Solidity files successfully
[sintan1071]% npm test

> monorepo-ethers-contracts@1.0.0 test
> hardhat run scripts/download-snark-artifacts.ts && hardhat test



  Feedback
    # joinGroup
      ✔ Should allow users to join the group (1402ms)
    # sendFeedback
      ✔ Should allow users to send feedback anonymously (3642ms)


  2 passing (9s)

[MacBook-Pro-2:contracts]
[sintan1071]% npm run test:coverage

> monorepo-ethers-contracts@1.0.0 test:coverage
> hardhat coverage


Version
=======
> solidity-coverage: v0.7.22

Instrumenting for coverage...
=============================

> Feedback.sol

Compilation:
============

Generating typings for: 12 artifacts in dir: ./build/typechain for target: ethers-v5
Successfully generated 40 typings!
Compiled 14 Solidity files successfully

Network Info
============
> HardhatEVM: v2.14.0
> network:    hardhat



  Feedback
    # joinGroup
      ✔ Should allow users to join the group (1550ms)
    # sendFeedback
      ✔ Should allow users to send feedback anonymously (3737ms)


  2 passing (9s)

---------------|----------|----------|----------|----------|----------------|
File           |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
---------------|----------|----------|----------|----------|----------------|
 contracts/    |      100 |      100 |      100 |      100 |                |
  Feedback.sol |      100 |      100 |      100 |      100 |                |
---------------|----------|----------|----------|----------|----------------|
All files      |      100 |      100 |      100 |      100 |                |
---------------|----------|----------|----------|----------|----------------|

> Istanbul reports written to ./coverage/ and ./coverage.json

[MacBook-Pro-2:contracts]
[sintan1071]% npm run test:report-gas

> monorepo-ethers-contracts@1.0.0 test:report-gas
> REPORT_GAS=true hardhat test

Compiled 14 Solidity files successfully

  Feedback
    # joinGroup
      ✓ Should allow users to join the group
    # sendFeedback
      ✓ Should allow users to send feedback anonymously

·-----------------------------|----------------------------|-------------|-----------------------------·
|     Solc version: 0.8.4     ·  Optimizer enabled: false  ·  Runs: 200  ·  Block limit: 30000000 gas  │
······························|····························|·············|······························
|  Methods                                                                                             │
·············|················|·············|··············|·············|···············|··············
|  Contract  ·  Method        ·  Min        ·  Max         ·  Avg        ·  # calls      ·  usd (avg)  │
·············|················|·············|··············|·············|···············|··············
|  Feedback  ·  joinGroup     ·     896130  ·     1656004  ·    1276067  ·            4  ·          -  │
·············|················|·············|··············|·············|···············|··············
|  Feedback  ·  sendFeedback  ·          -  ·           -  ·     396055  ·            2  ·          -  │
·············|················|·············|··············|·············|···············|··············
|  Deployments                ·                                          ·  % of limit   ·             │
······························|·············|··············|·············|···············|··············
|  Feedback                   ·          -  ·           -  ·    1514107  ·          5 %  ·          -  │
······························|·············|··············|·············|···············|··············
|  IncrementalBinaryTree      ·          -  ·           -  ·    1667044  ·        5.6 %  ·          -  │
······························|·············|··············|·············|···············|··············
|  Pairing                    ·          -  ·           -  ·    1204971  ·          4 %  ·          -  │
······························|·············|··············|·············|···············|··············
|  Semaphore                  ·          -  ·           -  ·    1846388  ·        6.2 %  ·          -  │
······························|·············|··············|·············|···············|··············
|  SemaphoreVerifier          ·          -  ·           -  ·    7357877  ·       24.5 %  ·          -  │
·-----------------------------|-------------|--------------|-------------|---------------|-------------·

  2 passing (10s)


```
