---
title: How to exclude specs or test files from webpack build in TS project
date: 2019-04-26
redirect_from: /how-to-exclude-specs-or-test-files-from-webpack-build-in-ts-project/
---
If you have your spec files in your **typescript project** but not the actual test runner you might be getting some weird errors. This might happen if you have in a monorepo environment or some similar situation.

This error is actually good one because usually you shouldn’t have tests within your build.

The errors you might get could be something like this:

```
ERROR in [at-loader] ./src/somefile.spec.tsx:2:25
TS2307: Cannot find module 'enzyme'.\n\nERROR in [at-loader] ./src/somefile.spec.tsx:3:26
TS2307: Cannot find module 'enzyme-to-json'.
 
﻿ERROR in [at-loader] ./src/somefile.spec.tsx:6:1
TS2304: Cannot find name 'describe'.\n\nERROR in [at-loader] ./src/somefile.spec.tsx:7:3
TS2304: Cannot find name 'it'.
 
ERROR in [at-loader] ./src/somefile.spec.tsx:10:5
TS2304: Cannot find name 'expect'.
 
ERROR in [at-loader] ./src/somefile.spec.tsx:14:5
TS2304: Cannot find name 'jest'.
```

So to fix the situation and remove the errors you have to exclude the spec files from the build. This should be done through typescript configuration (tsconfig.json). With the following style:

```
{
...
  "exclude": [
    "./src/**/*.spec.ts\",
    "./src/**/*.spec.tsx\",
    "node_modules\",
    "./dist/\" &lt;- or whatever you'r outDir path is
  ]
```

Remember that exclude array defaults to these locations:  
node\_modules, bower\_components, jspm\_packages and .