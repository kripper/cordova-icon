### Info of fixes:
- Android Icon fixes according to ([Android Adaptive Icons Guideline](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive?hl=de)). We are just deliver Icons in right sizes, having a padding within the icon.
- iOS Icons fixes according to iOS ([Human Interface Guideline for App-Icons](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/app-icon/)). We are delivering the missing sizes for cordova icons in iPhone/iPad Settings and Notifications.

# cordova-icon

<img src="cordova-icon-resize.png"/>

Automatic icon resizing for Cordova. Create an icon in the root folder of your Cordova project and use cordova-icon to automatically resize and copy it for all the platforms your project supports (currenty works with iOS, Android, Windows 10 and OSX).

This Project is forked from ([AlexDisler/cordova-icon](https://github.com/AlexDisler/cordova-icon)) and modified for cordova-android 8 and android sdk 28.

### Installation

```bash
$ sudo apt-get install imagemagick
$ # on Mac: brew install imagemagick
$ # on Windows: http://www.imagemagick.org/script/binary-releases.php#windows (check "Legacy tools")

$ sudo npm install cordova-icon-fix -g
```
If you are using an older version of cordova (before 7.x):

```bash
$ sudo npm install cordova-icon-fix@1.0.2 -g
```

### Requirements

- **ImageMagick installed**
- At least one platform was added to your project ([cordova platforms docs](http://cordova.apache.org/docs/en/edge/guide_platforms_index.md.html#Platform%20Guides))
- Cordova's config.xml file must exist in the root folder ([cordova config.xml docs](http://cordova.apache.org/docs/en/edge/config_ref_index.md.html#The%20config.xml%20File))

### Usage

Create an `icon.png` file in the root folder of your cordova project.
You can provide a platform-specific icon by naming it `icon-[platform].png`
(e.g `icon-android.png`, `icon-ios.png`).
Then run:

     $ cordova-icon-fix

You also can specify manually a location for your `config.xml` or `icon.png`:

     $ cordova-icon-fix --config=config.xml --icon=icon.png

If you run a old version of Cordova for iOS / Mac and you need your files in `/Resources/icons/`, use this option:

     $ cordova-icon-fix --xcode-old

For good results, your file should be:

- square
- for Android and iOS, at least 1024\*1024px
- for Windows, at least 1240\*1240px

#### Notes:

- Your `config.ml` file will not be updated by the tool (because images are automatically created in the good folders)
- Therefore, in your `config.xml`, be sure to remove all lines looking like `<icon src="res/android/ldpi.png" density="ldpi" />`

### Creating a cordova-cli hook

Since the execution of cordova-icon is pretty fast, you can add it as a cordova-cli hook to execute before every build.
To create a new hook, go to your cordova project and run:

    $ mkdir hooks/after_prepare
    $ vi hooks/after_prepare/cordova-icon.sh

Paste the following into the hook script:

    #!/bin/bash
    cordova-icon

Then give the script +x permission:

    $ chmod +x hooks/after_prepare/cordova-icon.sh

That's it. Now every time you `cordova build`, the icons will be auto generated.

### Splash screens

Check out [cordova-splash](https://github.com/AlexDisler/cordova-splash)


### License

MIT
