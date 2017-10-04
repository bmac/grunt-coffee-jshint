# grunt-coffee-jshint

[![npm version](https://badge.fury.io/js/grunt-coffee-jshint.svg)](https://badge.fury.io/js/grunt-coffee-jshint)
[![David dependency drift detection](https://david-dm.org/bmac/grunt-coffee-jshint.svg)](https://david-dm.org/bmac/grunt-coffee-jshint)

> Grunt wrapper for coffee-jshint

**NOTE: As of version `2.0.0`, `grunt-coffee-jshint` depends (through `coffee-jshint`) on [`coffeescript`](https://www.npmjs.com/package/coffeescript) in
favor of the, now deprecated, [`coffee-script`](https://www.npmjs.com/package/coffee-script) name.**


## Getting Started
This plugin requires Grunt `>=0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-coffee-jshint --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-coffee-jshint');
```

## The "coffee_jshint" task

### Overview
In your project's Gruntfile, add a section named `coffee_jshint` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  coffee_jshint: {
    options: {
      // Task-specific options go here.
    },
    your_target: {
      // Target-specific file lists and/or options go here.
    },
  },
});
```

### Options

#### `options.jshintOptions`
Type: `Array`
Default value: `[]`

A list of JSHint options to pass on as the `coffee-jshint --options option1,option2,option3,etc,...` argument.

For more information about these, please see [JSHint's options](http://jshint.com/docs/options).

#### `options.withDefaults`
Type: `Boolean`
Default value: `true`

If you want to turn off the default options for coffee-jshint, change this flag to `false`.

This is the equivalent of doing `coffee-jshint --default-options-off`.

For a list of coffee-jshint's defaults, please see its [options](https://github.com/marviq/coffee-jshint#options).

#### `options.globals`
Type: `Array`
Default value: `[]`

A list of all globals in the project.

This option is passed on as the `coffee-jshint --globals global1,global2,etc,...` argument.

See also [coffee-jshint's globals](https://github.com/marviq/coffee-jshint#globals).


### Usage Examples

#### Custom Options

In this example, some `globals` and `jshintOptions` are defined at the task level `options`, sometimes to be specifically replaced with target level
definitions.  For more information on what they do, please see JSHint's [Enforcing options](http://jshint.com/docs/options/#enforcing-options), [Relaxing
options](http://jshint.com/docs/options/#relaxing-options) and [Environments](http://jshint.com/docs/options/#environments). The latter group let `JSHint`
know about some pre-defined global variables so that you don't have to explicitly include them into `globals`.

```js
grunt.initConfig({
  coffee_jshint: {

    options: {

      globals: [

        'define',
        'IntersectionObserver',
        'Symbol'
      ],

      jshintOptions: [

        //  Environments:
        //
        'browserify'
        'browser'
        'devel'

        //  Enforcing options:
        //
        'eqeqeq',
        'forin',
        'noarg',
        'nonew',
        'undef',
        'unused',

        //  Relaxing options:
        //
        'debug',
        'loopfunc'
      ]
    },

    app: {
      files: [ ... ]
    },

    gruntfile: {

      options: {

        globals: [],

        jshintOptions: [

          //  Environments:
          //
          'node'
        ]
      },

      files: [ ... ]
    },

    test: {

      options: {

        jshintOptions: [

          //  Environments:
          //
          'jasmine',
          'node'

          //  Enforcing options:
          //
          //... likely copied from task level `options.jshintOptions`

          //  Relaxing options:
          //
          //... likely copied from task level `options.jshintOptions`
        ]
      }

      files: [ ... ]
    }
  }
});
```

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

### Prerequisites

  * [npm and node](https://nodejs.org/en/download/)
  * [jq](https://stedolan.github.io/jq/download/)


### Setup

Clone this repository somewhere, switch to it, then:

```bash
$ git config commit.template ./.gitmessage
$ npm install
```

This will:

  * Set up [a helpful reminder](.gitmessage) of how to make [a good commit message](#commit-message-format-discipline).  If you adhere to this, then a
    detailed, meaningful [CHANGELOG](./CHANGELOG.md) can be constructed automatically;
  * Install all required dependencies;


### Commit

#### Commit Message Format Discipline

This project uses [`conventional-changelog/standard-version`](https://github.com/conventional-changelog/standard-version) for automatic versioning and
[CHANGELOG](./CHANGELOG.md) management.

To make this work, *please* ensure that your commit messages adhere to the
[Commit Message Format](https://github.com/bcoe/conventional-changelog-standard/blob/master/convention.md#commit-message-format).  Setting your `git config` to
have the `commit.template` as referenced below will help you with [a detailed reminder](.gitmessage) of how to do this on every `git commit`.

```bash
$ git config commit.template ./.gitmessage
```


### Release

  * Determine what your next [semver](https://docs.npmjs.com/getting-started/semantic-versioning#semver-for-publishers) `<version>` should be:

    ```bash
    $ version="<version>"
    ```

  * Bump the package's `.version`, update the [CHANGELOG](./CHANGELOG.md), commit these, and tag the commit as `v<version>`:

    ```bash
    $ npm run release
    ```

  * If all is well this new `version` **should** be identical to your intended `<version>`:

    ```bash
    $ jq ".version == \"${version}\"" package.json
    ```

    *If this is not the case*, then either your assumptions about what changed are wrong, or (at least) one of your commits did not adhere to the
    [Commit Message Format Discipline](#commit-message-format-discipline); **Abort the release, and sort it out first.**


### Publish

#### To NPM

```bash
$ npm publish
```

#### On GitHub

```bash
git push --follow-tags --all
```

  * Go to [https://github.com/bmac/grunt-coffee-jshint/releases](https://github.com/bmac/grunt-coffee-jshint/releases);
  * Click the `Draft a new release` button;
  * Select the appropriate `v<version>` tag from the dropdown menu;

  * You could enter a title and some release notes here; at the very least include a link to the corresponding section in the [CHANGELOG](./CHANGELOG.md) as:
    ```markdown
    [Change log](CHANGELOG.md# ... )
    ```
  * Click the `Publish release` button;


## ChangeLog

See [CHANGELOG](./CHANGELOG.md).


## License

[MIT](LICENSE)
