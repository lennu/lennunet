---
title: vscode launch configurations for debugging and running jest tests
date: 2019-09-10
redirect_from: /vscode-launch-configurations-for-debugging-and-running-jest-tests/
---
If you use Jest and vscode it might get very slow and frustrating to run the tests always from the command line. With these launch configurations you can run single jest tests or all of them inside vscode.

You can add the configuration from here:

{% image "./vscode-debugging.png", "vscode debugging" %}

The file will most probably be located inside your workspace at the root level: `your-project/.vscode/launch.json` – this is where vscode is looking for the config and you can even create the folder and file yourself.

The following snippet has my usual launch config for projects using jest. It includes two different configurations – one for running just the current file and one for running all the tests.

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Jest Current File",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": [
        "${fileBasenameNoExtension}",
        "--config",
        "${workspaceRoot}/jest.config.js"
      ],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen",
      "disableOptimisticBPs": true
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Jest All",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": [
        "--config",
        "${workspaceRoot}/jest.config.js"
      ],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen",
      "disableOptimisticBPs": true
    }
  ]
}
```

After this you can open up Jest files and press `F5` which will start the “debugging” in vscode. Just remember to choose the right configuration from the dropdown menu.