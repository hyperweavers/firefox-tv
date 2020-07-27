# Firefox for Android TV

_Fast for good, just right for watching video at home. A browser for
discovering and watching web video on the big screen TV for users to install on
their Android TV._

## Build instructions
Dependencies:
- Java 8, *not the latest version* (for building via the command line)

1. Clone the repository:

  ```shell
  git clone https://github.com/k7moorthi/firefox-tv
  ```

2. Import the project into Android Studio or build on the command line:

  ```shell
  ./gradlew clean app:assembleSystemDebug
  ```

3. Make sure to select the right build variant in Android Studio: **systemDebug**

### Running
It is recommended to test directly on a Android TV:
You can connect with:
```shell
adb connect <IP address>:5555
```

And then install via Android Studio or adb. Only a single development device
can be connected to a Android TV at a time. Note that while you can install on an
Android TV emulator, the behavior (particularly `WebView` behavior) is different 
from Android TV's and should not be relied upon.

If using an emulator, we recommend the Android TV device image: either 720p or
1080p is fine. API 22 and 25 are best. You can press `cmd + m` to
simulate a menu button press.

### Unit Testing
To run a reasonable subset of the unit tests, we recommend:
```sh
./gradlew testSystemDebug
```

To generate code coverage reports, run:
```sh
./gradlew -Pcoverage jacocoDebugTestReport
```

Reports can be found at `app/build/jacoco/jacoco<buildVariant>TestReport/html/index.html`

### UI Testing
To run all UI tests, follow these steps

1. Connect to one device
  - Either use `adb connect` for a real device, or start an emulator instance using AVD
  - Prefer a real device (emulators will fail some tests)
  - The next step will fail if you are connected to more than one device
2. Run `./gradlew connectedSystemDebugAndroidTest` from the command line
  - Aliasing this command is recommended

### Building release builds
Release builds can be built in Android Studio or via the command line:
```sh
./gradlew assembleSystemRelease # unsigned build
```

These builds will run validation checks that the build is ready for a production release. If you
do not want to run these checks (e.g. building release builds for local debugging), you can add this
argument:
```sh
./gradlew assembleSystemRelease -PnoValidate
```
## License

    This Source Code Form is subject to the terms of the Mozilla Public
    License, v. 2.0. If a copy of the MPL was not distributed with this
    file, You can obtain one at http://mozilla.org/MPL/2.0/
