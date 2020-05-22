# Overview


# package.json

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

# Package Versions

- Major.Minor.Patch
    + Major: making incompatible API changes
    + Minor: backwards-compatible changes
    + Patch: backwards-compatible bug fixes
- Range
    + "2" = "2.x.x"
    + "2.x"
    + "~1.2.3": greater than or equal to 1.2.3 and less than 1.3.0
    + "^1.2.3": greater than or equal to 1.2.3 and less than 2.0.0

# npm: Node Package Manager

## Packages and Modules

## Commands

### Installation

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
- `npm install <module> --global`: install a module globally

# Tips and Tricks

## Commands

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
