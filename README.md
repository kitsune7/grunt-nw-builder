# grunt-nw-builder [![NPM version][npm-image]][npm-url]

> Let's you build your [NW.js](https://github.com/nwjs/nw.js) apps for OSX, Windows, and Linux with Grunt. It will download the prebuilt binaries for the specified version, unpack it, create a release folder, create an `app.nw` file, and copy `app.nw` to where it belongs.

*Issues with the output should be reported on the nw-builder [issue tracker](https://github.com/mllrsohn/nw-builder/issues).

## Getting Started
This plugin requires Grunt `^1.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you can install this plugin with the following command:

```shell
npm install @happikitsune/grunt-nw-builder --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-nw-builder');
```

## The "nwjs" task


### Usage Examples

```js
grunt.initConfig({
  nwjs: {
    options: {
        platforms: ['win','osx'],
        buildDir: './webkitbuilds', // Where the build version of my NW.js app is saved
    },
    src: ['./example/public/**/*'] // Your NW.js app
  },
})
```


### Options

Exactly the same as [nw-builder](https://github.com/mllrsohn/nw-builder). You have the advantage of configuring the files via Grunt.

## Manifest Options

### platformOverrides

Just like [nw-builder](https://github.com/mllrsohn/nw-builder#manifest-options) you can specify platform-specific manifest values.

```json
{
    "name": "nw-demo",
    "version": "0.1.0",
    "main": "index.html",
    "window": {
        "frame": false,
        "toolbar": false
    },
    "platformOverrides": {
        "win": {
            "window": {
                "frame": true
            }
        }
    }
}
```

For more information see nw-builder's [Manifest Options](https://github.com/mllrsohn/nw-builder#manifest-options).

## Troubleshooting

### OSX ulimit

Darwin (OS X kernel) has a low limit for file descriptors (256 per process) by default, so you might get an `EMFILE` error or an error mentioning "too many open files" if you try to open more file descriptors than this.

To get around it, run `ulimit -n 1024` (or add it to your `~/.bash_profile`). For more information, see [henvic/osx-ulimit](https://github.com/henvic/osx-ulimit).


## Release History
- 2021-08-05    `3.5.7` Changing the version to match the latest version of `nw-builder` to date
- 2016-09-14    `flavor` option; you can now select any flavor of NW.js, not just `sdk`.
- 2016-08-28    bumping nw-builder dependency to 3.0.0.
- 2016-07-02    `2.0.3` Fix for zip option plus some small `nw-builder` fixes.
- 2016-07-02    `2.0.2` Updated Grunt peer dependency
- 2016-07-02    `2.0.1` Supporting newer NW.js versions, alpha/beta builds, plus some other small fixes.
- ...
- 2014-12-12    `1.0.0` 64-bit support, improved platform-overrides and no more EMFILE errors. Also, macPlist CFBundleIdentifier is generated from `package.json`.
- 2014-08-01    `0.3.0` macPlist option improvements (see [mllrsohn/nw-builder#96](https://github.com/mllrsohn/nw-builder/pull/96))
- 2014-08-01    `0.2.0` Moved logic into a separate [module](https://github.com/mllrsohn/nw-builder), config options will be backward compatible except `keep_nw` is no longer supported
- 2013-09-19    Removed config merging (but kept the lookup for version number and name), added keep_nw option, fixed various small bugs.
- 2013-09-09    Fixed accidental deletion of nw.exe on Windows builds, adding several improvements, opt in for timestamped builds, using version and name from package.json to name the build product and build dir, renamed download directory to `cache`, added merge from package.json options for nodewebkit (no need to add configuration to Gruntfile, but stays optional)
- 2013-08-20    Fix for the `unzip` lib
- 2013-08-13    Initial release

[npm-url]: https://npmjs.org/package/@happikitsune/grunt-nw-builder
[npm-image]: https://img.shields.io/npm/v/@happikitsune/grunt-nw-builder
