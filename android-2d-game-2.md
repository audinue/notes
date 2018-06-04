# Android 2D Game Development Notes 2

## Preparing your phone

1. Disable screen lock
2. Enable USB debugging
3. Connect your phone to your laptop
4. Open `run.cmd`
5. Type `adb devices`

## Creating new project

1. Double click `run.cmd`
2. Type `android create project -n HelloWorld -a HelloWorld -k io.github.audinue.helloworld -t 1 -p HelloWorld`

```
                         Action "create project":
  Creates a new Android project.
Options:
 -n --name          : Project name.
 -a --activity      : Name of the default Activity that is created.
                      [required]
 -k --package       : Android package name for the application. [required]
 -v --gradle-version: Gradle Android plugin version.
 -t --target        : Target ID of the new project. [required]
 -g --gradle        : Use gradle template.
 -p --path          : The new project's directory. [required]
```

## Building and running your project

1. Type `cd HelloWorld`
2. Type `ant debug` to build your app
3. Type `ant installd` to install your app on your phone
4. Type `adb shell am start -n io.github.audinue.helloworld/.HelloWorld` to start the activity
5. Type `adb shell input keyevent KEYCODE_POWER` to turn on your phone. This command doesn't work over the air.

Done!
