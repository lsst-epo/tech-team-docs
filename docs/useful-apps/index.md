# Useful Apps

### Docker

Several of our projects are run with Docker locally and in production. Docker configuration and scripting is fairly complicated, but [installing the docker client and running containers is fairly straight-forward](https://docs.docker.com/get-docker/).

### Adobe Creative Cloud

Our team's Designer delivers web designs exclusively in Adobe file formats, principally as InDesign or Illustrator files, and XD prototypes.

### PixelSnap

[PixelSnap](https://getpixelsnap.com) is a super useful tool that does 1 thing very well: pixel-accurate measurements of your screen. We find this to be invaluable when translating design into code: the ability to compare measurements in XD to those in the browser allows you to quickly and easily verify layouts you defined in stylesheets match those a designer created by hand.

### Color Picker

The native Apple Color Picker utility is absent in recent macOS versions.  But there are many many many excellent free replacement options.  [System Color Picker](https://sindresorhus.com/system-color-picker) is one of them.  It includes an eye dropper tool which is the most critical feature as, similarly to PixelSnap, it enables you to verify color choices in design are accurately translated to code.  For instance, one common gotcha is that designers often create many shades of a color by shifting its opacity.  Replicating those colors in the same way in the browser (i.e. by shifting opacity) is not usually the preferred approach.  Using an eye dropper tool in a Color Picker app allows you to grab the hex or rgba color code from the pixel on the screen itself, and therefore reproduce it 1:1 in code.

### Xcode

If you installed Homebrew you likely already have access to the Xcode Command Line Tools.  This is typically sufficient for most every kind of Xcode-y apple developy thing you need to do, with one important exception: emulating iPhones.  To emulate an iPhone on your Apple you need to install the full [Xcode 13 app](https://developer.apple.com/xcode/).  Xcode also enables you to use browser-based devTools with a tethered iPhone.  While there is no substitute for testing on a real device, the Xcode emulated iPhone will tend to catch more mobile-specific issues than testing in the Chrome browser-based emulator alone.

### Genymotion

[Genymotion](https://www.genymotion.com/download/) is an Android device emulator.  This allows you to test on mobile on Android.  It also supports "tethering" the emulated device to chrome, so you can use the Chrome DevTools with the emulated device.  There are many similar apps out there that accomplish this, Ganymotion happens to be free and primarily has been chosen for that reason.

### 1Password

[1Password](https://support.1password.com/getting-started-mac/) is our team's preferred Password Manager. It is a repository for all of the credentials you use across the internet, or in local software. It natively, and via browser extensions, supports autofilling form fields. It is also a 2-factor Authorizer, which means you can use it whenever an online service requires an app-based (as oppose to SMS-based) 2-factor authentication.

### Chronos

We use Jira as our main project management, ticketing, and time tracking tool.  [Chronos](https://chronos.web-pal.com/) is a free app that allows you to manage, edit, and log time in Jira tickets via a desktop app.  Additionally, it features realtime time tracking for wok logs so that you can track the time you are taking to do something, rather than estimate time spent in advance or after the fact.

### BlueJeans

[BlueJeans](https://www.bluejeans.com/) is the official audio/video conferencing tool for the Rubin Project.  Whereas...

### Zoom

[Zoom](https://zoom.us/) is the official audio/video conferencing tool for NOIRLab.  So you'll def need both.
