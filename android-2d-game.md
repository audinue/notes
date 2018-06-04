# Android 2d Game Development Notes

## Installing SDK

1. Download [Android SDK v25](https://dl.google.com/android/repository/tools_r25.2.5-windows.zip).
2. Extract it to&mdash;for example&mdash; `D:\android`.
3. Double click `android.bat`
4. **Deselect** all first.
5. Select `Android SDK Build-tools` version **26.03**
6. Select `Android 4.4.2 (API 19) > SDK Platform`... I'm developing for KitKat.
7. Click Install Packages.

## Installing Apache Ant

1. Download [Apache Ant](http://www-us.apache.org/dist//ant/binaries/apache-ant-1.10.3-bin.zip).
2. Extract it to `D:\android\ant`

## Create Development Environment

Create a new BAT/CMD file under `D:\android`.

```
@ECHO OFF

SET ANDROID_HOME=%~dp0
SET PATH=%PATH%;%~dp0tools;%~dp0platform-tools;%~dp0ant\bin

CMD /K
```
