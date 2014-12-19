# grunt-file-dependencies

> Generates a list of files in dependency order.

You may want to use this plugin if the following applies to your project:
* You are not using the AMD patter and are not using a module script loader (like [RequireJS](http://requirejs.org/)) that provides dependency loading
  * modules create closure, closure requires extra time/memory overhead for every instance of a class, you need every bit of efficiency you can get
  * you have your reasons
* The source code is separated into several source files (e.g. classes) that depend on each other and need to be loaded in the correct order
* You want to use a script tag injection plugin during development for easy debugging (e.g. [grunt-sails-linker](https://www.npmjs.com/package/grunt-sails-linker) but it has no clue about the file dependencies
* You want to use a concatenation plugin for a release build (e.g. [grunt-contrib-concat](https://www.npmjs.com/package/grunt-contrib-concat)) but it has no clue about the file dependencies


## Getting Started
This plugin requires Grunt `~0.4.5`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-file-dependencies --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-file-dependencies');
```

## The "file_dependencies" task

### Overview
In your project's Gruntfile, add a section named `file_dependencies` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  file_dependencies: {
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

#### options.outputProperty,
Type: `String`
Default value: `'file_dependencies.current_target.ordered_files'`

The name of the grunt config property which will be assigned the array of ordered file paths. The default is to set the `ordered_files` property on the current task's configuration.

#### options.outputFile
Type: `String`
Default value: `''`

The name of a file that will be created with the array of ordered file paths.

#### options.extractDefinesRegex
Type: `RegExp`
Default value: `/define\s*\(\s*['"]([^'"]+)['"]/g`

A regular expression used to search each file for the name of a dependency definition (e.g. class definition).

#### options.extractRequiresRegex
Type: `RegExp`
Default value: `/require\s*\(\s*['"]([^'"]+)['"]/g`

A regular expression used to search each file for the name of a dependency requirement (e.g. class requirement).

### Usage Examples

#### Default Options
In this example, the default options are used to do something with whatever. So if the `testing` file has the content `Testing` and the `123` file had the content `1 2 3`, the generated result would be `Testing, 1 2 3.`

```js
grunt.initConfig({
  file_dependencies: {
    options: {},
    files: {
      'dest/default_options': ['src/testing', 'src/123'],
    },
  },
});
```

#### Custom Options
In this example, custom options are used to do something else with whatever else. So if the `testing` file has the content `Testing` and the `123` file had the content `1 2 3`, the generated result in this case would be `Testing: 1 2 3 !!!`

```js
grunt.initConfig({
  file_dependencies: {
    options: {
      separator: ': ',
      punctuation: ' !!!',
    },
    files: {
      'dest/default_options': ['src/testing', 'src/123'],
    },
  },
});
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_
