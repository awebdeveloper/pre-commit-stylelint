Pre-commit hook for Styleint  
=============================

This is the Stylelint hook for [pre-commit](https://github.com/pre-commit/pre-commit). This prevents git commits unless the checks pass. 


### Using styleint with pre-commit

- To use this you first need to install pre-commit(see links below). 
- Then create a pre-commit config file and also a stylelint config file in the root of your project. 
- Run `pre-commit install` from the root of your project

Finally add this to your `.pre-commit-config.yaml`:

```yaml
-   repo: https://github.com/awebdeveloper/pre-commit-stylelint
    rev: '' # Use the sha or tag you want to point at like 0.0.1
    hooks:
    -   id: stylelint
        additional_dependencies: ['stylelint@13.2.1', 'stylelint-config-standard@20.0.0'] //specify the latest version
 ```
PS: These are for version 2.3.0 visit https://pre-commit.com/#2-add-a-pre-commit-configuration for latest config syntax or for config syntax specific to your version

 Now everytime you commit a scss/css file. It will run stylelint on this and prevent commit if the checks fail.
 
 ### Stylelint 17 and later

From v17, Stylelint can't find packages from `additional_dependencies` when your config refers to them by name in `extends`, `plugins` or `customSyntax`, and every file fails with:

```
ConfigurationError: Could not find "stylelint-config-standard". Do you need to install the package or use the "configBasedir" option?
```

pre-commit installs `additional_dependencies` into the hook's own environment and puts its `node_modules` folder on `NODE_PATH`. Stylelint 16 searched `NODE_PATH` as a fallback, but Stylelint 17 dropped that fallback ([stylelint/stylelint#8886](https://github.com/stylelint/stylelint/pull/8886)) and only looks in `node_modules` folders above your config file.

You can work around this with a JavaScript config that resolves the package paths itself, since Node's `require.resolve` still reads `NODE_PATH`:

```js
// stylelint.config.mjs
import fs from "node:fs";
import { createRequire } from "node:module";
import path from "node:path";

const require = createRequire(import.meta.url);

function resolve(name) {
  try {
    return require.resolve(name);
  } catch {
    // ESM-only packages such as stylelint-config-standard-scss can't be
    // resolved by require, so point Stylelint at their index.js instead.
    return (
      require.resolve
        .paths(name)
        ?.map((dir) => path.join(dir, name, "index.js"))
        .find((file) => fs.existsSync(file)) ?? name
    );
  }
}

export default {
  extends: [resolve("stylelint-config-standard-scss")],
};
```

This still uses your project's `node_modules` first when the packages are installed there, so running `npx stylelint` and editor integrations keep working. It won't find an ESM-only package whose entry point is somewhere other than `index.js` at the package root.

 ### Links
 - For pre-commit: see https://github.com/pre-commit/pre-commit

 - For stylelint: see http://stylelint.io/


