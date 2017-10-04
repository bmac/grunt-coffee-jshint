# grunt-coffee-jshint

> grunt wrapper for coffee-jshint

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

#### options.jshintOptions
Type: `Array`
Default value: `[]`

A list of options for coffee-jshint.
For more informations, please see coffee-jshint's [Options](https://github.com/marviq/coffee-jshint#options)

#### options.withDefaults
Type: `Boolean`
Default value: `true`

If you want to turn off the default options for coffee-jshint, change this flag to `false`.
For more informations, please see coffee-jshint's [Options](https://github.com/marviq/coffee-jshint#options)

#### options.globals
Type: `Array`
Default value: `[]`

A list of all globals in the project.

### Usage Examples

#### Custom Options

In this example, some `globals` and `jshintOptions` are defined at the task level `options`, sometimes to be specifically relpaced with target level
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

## Release History
_(Nothing yet)_
