# Overview

- Best practices
    + Install all packages locally: `npm install pkg`
    + Run the local binaries: `npx <cmd> [args]`

# npm CLI

## Commands

- Update npm: `npm install -g npm@latest`
    + `npm i -g npm@latest`
- `npm init`: step-by-step to scaffold a project
    + name, version, description, main file, test command, git
    repository link, keywords, license
    + `npm init --yes` for all default values
- `npm install <module>`: install a module to the current directory
  without saving to `package.json`
- `npm install <module> --save`: install a module to the current
  directory and save it to `dependencies` in `package.json`
- `npm install <module> --save-dev`: install a module to the current
  directory and save it to `devDependencies` in `package.json`
- `npm install`: install all modules in `dependencies` and
  `devDependencies` in `package.json` to the current directory
    + If `package.json` is not manually modified and there are
      `package-lock` or `shrinkwrap` files, the installation will be
      driven by `package-lock` or `shrinkwrap` files.
    + If `package.json` is manually modified and incompatible with
      `package-lock`, then the `package-lock` will be updated with the
      new data in `package.json`, and the installation is driven by
      `package.json`.
    + https://github.com/npm/npm/issues/17979
    + https://docs.npmjs.com/cli/v8/commands/npm-ci
- `npm install <module> --global`: install a module globally
- View an installed package's info:
    + All info: `npm view <pkg>`
    + Version: `npm view <pkg> version`
- List all installed packages
    + Local packages: `npm list`
    + Global packages: `npm list -g`
        * If you use old npm version: `npm list -g --depth=0`
- Open a package's homepage: `npm home <pkg>`
- Open a package's git repo: `npm repo <pkg>`
- Check outdated dependencies: `npm outdated`
- Prune packages that are not in `package.json`: `npm prune`
- Lock down dependencies version for publication: `npm shrinkwrap`
- Change default save prefix to `~`: `npm config set save-prefix="~"`
    + `~`: only allow update patches => more safe
    + `^`: allow updating minor
- Set some defaults:
    + `npm config set init.author.name $name`
    + `npm config set init.author.email $email`
- `npm run-script`
    + https://docs.npmjs.com/cli/v8/commands/npm-run-script
    + Run arbitrary package script
    + Aliases: `run, rum, urn`

### npm cheat sheet

- Install a package and also update package.json with the installed
  version and package name.
    + `npm install <module-name> --save`
- Install a package and also update package.json with the installed
  version and package name, but into the devDependencies section.
    + `npm install <module-name> --save-dev`
- Set --save as a default for `npm install`.
    + `npm config set save true`
- Generate package.json in a module directory, based on npm parmaters.
    + `npm init`
- List all npm configuration flags.
    + `npm config ls -l`
- Install a version not from a git repository and not from the npm
  directory, for example:
    + `npm install git://github.com/substack/node-browserify.git`
- Update the global npm version.
    + `npm update npm -g`
- Display the readme.md / documentation / npmjs.orf page of a give library.
    + `npm docs <module-name>`
- Run package test suite, based on setup in package.json in:
    + `"scripts" : {"test" : "node testfile.js"}`
    + `npm test`
- Uninstall package (A nice thing about npm is you can always just `rm -rf ./node_modules/<module_name>`).
    + `npm uninstall <module_name>`
- Locally edit a dependency.
    + `npm edit <module_name>`
- Setup editor for `npm edit` :
    + `npm config set editor "sublime"`
- Publish a package not under the default "latest" tag:
    + `npm publish --tag beta`
- List outdated libraries compared to currently installe node_modules:
    + `npm outdated`
- Lock down dependency versions:
    + `npm shrinkwrap`
- Install a git specific release
    + `npm install git://github.com/Marak/colors.js#v0.6.0`

## Configuring npm

### Summary

- Since `package-lock.json` is committed with this package, you should
  use `npm ci` to install packages from `package-lock.json` instead of
  using `npm install` which will install packages from `package.json`
  and update the `package-lock.json` if there is mismatch between
  `package-lock.json` and `package.json`
- If you want to add dependencies, then you should modify `package.json`
  and run `npm install` to update `package-lock.json`, then commit the
  changes for both `package.json` and `package-lock.json`.
- If there is conflict when you add dependencies because somebody also
  does the same thing, then you should resolve the conflict in
  `package.json`, then rerun `npm install` to update
  `package-lock.json`, and then continue with the merge of your changes
  to the code base.

### package.json

- `package.json`: list of all packages that the project depends on
    + metadata of the project: name, version, description, license,
    keywords
    + devDependencies: dependencies of the development phase
    + dependencies: the production phase

```
{
  "name": "metaverse",
  "version": "0.92.12",
  "description": "The Metaverse virtual reality. The final outcome of all virtual worlds, augmented reality, and the Internet.",
  "main": "index.js"
  "license": "MIT",
  "devDependencies": {
    "mocha": "~3.1",
    "native-hello-world": "^1.0.0",
    "should": "~3.3",
    "sinon": "~1.9"
  },
  "dependencies": {
    "fill-keys": "^1.0.2",
    "module-not-found-error": "^1.0.0",
    "resolve": "~1.1.7"
  }
}
```

### package-lock.json


## Using npm

### Scripts

- https://docs.npmjs.com/cli/v8/using-npm/scripts

# Package Versions (Semantic Version, semver)

- Major.Minor.Patch
    + Major: making incompatible API changes
    + Minor: backwards-compatible changes
    + Patch: backwards-compatible bug fixes
- Range
    + "2" = "2.x.x"
    + "2.x"
    + "~1.2.3": greater than or equal to 1.2.3 and less than 1.3.0
    + "^1.2.3": greater than or equal to 1.2.3 and less than 2.0.0

# Packages and Modules


# Dependencies

- Peer Dependencies
    + https://nodejs.org/es/blog/npm/peer-dependencies/
    + https://flaviocopes.com/npm-peer-dependencies/
    + It's not automatically install
    + It's usually used in library package
    + These dependencies are needed in the dependencies of the
      application package that uses the library package.


# Best Practices

- Pin your dependencies if your package is not a library
- Library packages can use ranges for dependencies but pin development
  dependencies.
- Use a lock file


# Tips and Tricks

## Update dependencies

- https://www.npmjs.com/package/npm-check-updates
- Check dependencies' new versions
    + `npx npm-check-updates`
    + Red = major upgrade (and all major version zero)
    + Cyan = minor upgrade
    + Green = patch upgrade
- Check upgrade a package
    + `npx npm-check-updates <package-name>`
- Check upgrade multiple packages: chalk, mocha, and react
    + `npx npm-check-updates chalk mocha react`
- Check upgrade packages that start with "react-"
    + `npx npm-check-updates react-*`
    + `npx npm-check-updates "/^react-.*$/"`
- Check upgrade everything except nodemon
    + `npx npm-check-updates \!nodemon`
- Check upgrade everything except packages that do not start with "react-"
    + `npx npm-check-updates \!react-*`
- Only check upgrade patch and minor:
    + `npx npm-check-updates --target minor`
- Only check upgrade patch
    + `npx npm-check-updates --target patch`

TO REALLY UPGRADE PACKAGES, ADD `-u` TO THE COMMAND TO UPGRADE

Peru
    + https://sage.amazon.com/posts/1233317
