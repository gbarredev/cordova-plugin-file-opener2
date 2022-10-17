# A File Opener Plugin for Cordova

[![Latest Stable Version](https://img.shields.io/npm/v/cordova-plugin-file-opener2.svg)](https://www.npmjs.com/package/cordova-plugin-file-opener2) [![Total Downloads](https://img.shields.io/npm/dt/cordova-plugin-file-opener2.svg)](https://npm-stat.com/charts.html?package=cordova-plugin-file-opener2)

This plugin will open a file on your device file system with its default application.

```js
cordova.plugins.fileOpener2.open(
    filePath,
    fileMIMEType,
    {
        error : function(){ },
        success : function(){ }
    }
);
```

## Installation

```shell
$ cordova plugin add cordova-plugin-file-opener2
```

### Optional variables

This plugin requires the Android support library v4. From release `2.1.0` the version of this can be set at installation. The minimum version is `24.1.0`. Default value is `27.+`. [Check out the latest version](https://developer.android.com/topic/libraries/support-library/revisions.html).

```shell
$ cordova plugin add cordova-plugin-file-opener2  --variable ANDROID_SUPPORT_V4_VERSION="27.+"
```

If you are using the `cordova-android-support-gradle-release` plugin it should match the value you have set there.

## Requirements

The following platforms and versions are supported by the latest release:

- Android 4.4+ / iOS 9+ / Windows / Electron
- Cordova CLI 7.0 or higher

Cordova CLI 6.0 is supported by 2.0.19, but there are a number of issues, particularly with Android builds (see [232](https://github.com/pwlin/cordova-plugin-file-opener2/issues/232) [203](https://github.com/pwlin/cordova-plugin-file-opener2/issues/203) [207](https://github.com/pwlin/cordova-plugin-file-opener2/issues/207)). Using the [cordova-android-support-gradle-release](https://github.com/dpa99c/cordova-android-support-gradle-release) plugin may help.


## fileOpener2.open(filePath, mimeType, options)

Opens a file

### Supported Platforms

- Android 4.4+
- iOS 9+
- Windows
- Electron

### Quick Examples
Open a PDF document with the default PDF reader and optional callback object:

```js
cordova.plugins.fileOpener2.open(
    '/Download/starwars.pdf', // You can also use a Cordova-style file uri: cdvfile://localhost/persistent/Downloads/starwars.pdf
    'application/pdf',
    {
        error : function(e) {
            console.log('Error status: ' + e.status + ' - Error message: ' + e.message);
        },
        success : function () {
            console.log('file opened successfully');
        }
    }
);
```

__Note on Electron:__ Do not forget to enable Node.js in your app by adding `"nodeIntegration": true` to `platforms/electron/platform_www/cdv-electron-settings.json` file, See [Cordova-Electron documentation](https://cordova.apache.org/docs/en/latest/guide/platforms/electron/index.html#customizing-the-application's-window-options).


## fileOpener2.showOpenWithDialog(filePath, mimeType, options)

Opens with system modal to open file with an already installed app.

### Supported Platforms

- Android 4.4+
- iOS 9+

### Quick Example

```js
cordova.plugins.fileOpener2.showOpenWithDialog(
    '/Downloads/starwars.pdf', // You can also use a Cordova-style file uri: cdvfile://localhost/persistent/Downloads/starwars.pdf
    'application/pdf',
    {
        error : function(e) {
            console.log('Error status: ' + e.status + ' - Error message: ' + e.message);
        },
        success : function () {
            console.log('file opened successfully');
        },
        position : [0, 0]
    }
);
```
`position` array of coordinates from top-left device screen, use for iOS dialog positioning.


## Notes

- For properly opening _any_ file, you must already have a suitable reader for that particular file type installed on your device. Otherwise this will not work.

- [It is reported](https://github.com/pwlin/cordova-plugin-file-opener2/issues/2#issuecomment-41295793) that in iOS, you might need to remove `<preference name="iosPersistentFileLocation" value="Library" />` from your `config.xml`

- If you are wondering what MIME-type should you pass as the second argument to `open` function, [here is a list of all known MIME-types](http://svn.apache.org/viewvc/httpd/httpd/trunk/docs/conf/mime.types?view=co)


---


