# Cordova Background Geolocation Plugin

[![npm](https://img.shields.io/npm/v/@diotoborg/nam-quod?style=flat-square)](https://www.npmjs.com/package/@diotoborg/nam-quod)
![npm downloads](https://img.shields.io/npm/dm/@diotoborg/nam-quod?style=flat-square)

[![GitHub issues](https://img.shields.io/github/issues/HaylLtd/@diotoborg/nam-quod?style=flat-square)](https://github.com/HaylLtd/@diotoborg/nam-quod/issues)
[![GitHub stars](https://img.shields.io/github/stars/HaylLtd/@diotoborg/nam-quod?style=flat-square)](https://github.com/HaylLtd/@diotoborg/nam-quod/stargazers)
![GitHub last commit](https://img.shields.io/github/last-commit/HaylLtd/@diotoborg/nam-quod?style=flat-square)

## Introduction

*Cross-platform geolocation for Cordova and Capacitor with battery-saving "circular region monitoring" and "stop detection"*

This plugin can be used for geolocation when the app is running in the foreground or background. It is more battery and data efficient than html5 geolocation. It can be used side by side with other geolocation providers (eg. html5 navigator.geolocation).

This project is based on [@mauron85/cordova-plugin-background-geolocation](https://github.com/mauron85/cordova-plugin-background-geolocation), which in turn was based on the original [cordova-background-geolocation plugin](https://github.com/christocracy/cordova-plugin-background-geolocation) by [christocracy](https://github.com/christocracy). Hayl Ltd have taken on responsibility for hosting it and will be maintaining it and merging PRs from the community. If you have any fixes, features or updates that you would like included, please do raise a PR or issue on the GitHub repository.

**ATENTION:** This project changes the package name from it's parents. The words are the same but in a different order, which is easy to miss and can cause some confusion

We are also looking to maintainers to help with this, so that the project does not end up orphaned. If you are interested in helping out with maintaining the project, please see the [pinned discussion at GitHub](https://github.com/HaylLtd/@diotoborg/nam-quod/discussions/3).

The NPM package can be found at [@diotoborg/nam-quod](https://www.npmjs.com/package/@diotoborg/nam-quod).

<font size="4">[Documentation](https://haylltd.github.io/@diotoborg/nam-quod/)</font>

### Installing the plugin

**Note:** for non AndroidX project please use version 1.x of this plugin. Version 2.x and on will support AndroidX.

**Note:** this plugin can be installed on a Capacitor project and it is tested to be working as expected, some configuration may need to be done differently than below according to how Capacitor configuration is implemented.

**Note:** for Android 14+ there's a need to let Google know why the app needs to use the location and have a video link when uploading for the first time to play console. It takes some time to approve and after that there's no need to do it again. This is related to `FOREGROUND_SERVICE_LOCATION` premission.

**Note:** for Android 13+ there's a need for runtime `POST_NOTIFICATION` permission request in order to show the icon.


```bash
npm install @diotoborg/nam-quod
npx cap sync
```

```bash
cordova plugin add @diotoborg/nam-quod
```

You may also want to change default iOS permission prompts and set specific google play version and android support library version for compatibility with other plugins.

**Note:** Always consult documentation of other plugins to figure out compatible versions.

```bash
cordova plugin add @diotoborg/nam-quod \
  --variable GOOGLE_PLAY_SERVICES_VERSION=11+ \
  --variable ALWAYS_USAGE_DESCRIPTION="App requires ..." \
  --variable MOTION_USAGE_DESCRIPTION="App requires motion detection"
```

**Note:** To apply changes, you must remove and reinstall plugin.

### Usage

First, configure the plugin with the settings you require.

```js
BackgroundGeolocation.configure({
    locationProvider: BackgroundGeolocation.ACTIVITY_PROVIDER,
    desiredAccuracy: BackgroundGeolocation.HIGH_ACCURACY,
    stationaryRadius: 50,
    distanceFilter: 50,
    notificationTitle: 'Background tracking',
    notificationText: 'enabled',
    debug: true,
    interval: 10000,
    fastestInterval: 5000,
    activitiesInterval: 10000,
    url: 'http://192.168.81.15:3000/location',
    httpHeaders: {
      'X-FOO': 'bar'
    },
    // customize post properties
    postTemplate: {
      lat: '@latitude',
      lon: '@longitude',
      foo: 'bar' // you can also add your own properties
    }
  });
```

Then call `start()` to start location tracking.

A more comprehensive example can be found in the [Documentation](https://haylltd.github.io/@diotoborg/nam-quod/example)

### Compatibility

| Plugin version   | Cordova CLI       | Cordova Platform Android | Cordova Platform iOS |
|------------------|-------------------|--------------------------|----------------------|
| >1.0.0           | 8.0.0             | 8.0.0                    | 6.0.0                |
| >2.0.0           | 10.0.0            | 10.0.0                   | 6.0.0                |

## Licence

[Apache License](http://www.apache.org/licenses/LICENSE-2.0)

Copyright (c) 2013 Christopher Scott, Transistor Software

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
