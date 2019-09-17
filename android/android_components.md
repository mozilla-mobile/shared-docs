# Building android-components #

## Preparation ##

1. Install Android Studio if it is not yet installed. This will also install a JDK.
2. Find out where Android Studio installed the JDK by:
    1. Opening Android Studio.
    2. Selecting "Configure."
    3. Selecting "Default Project Structure".
    4. You should now see the Android JDK location. (On OS X, mine is `/Applications/Android Studio.app/Contents/jre/jdk/Contents/Home`.)
3. Set the environment variable `JAVA_HOME` to the path of the JDK. I did this on OS X by adding the line `# export JAVA_HOME="/Applications/Android Studio.app/Contents/jre/jdk/Contents/Home"` to `.bash_profile`.
4. Close Android Studio.

## Installation ##

1. Clone the repo with the command: `git clone https://github.com/mozilla-mobile/shared-docs.git`
2. Open Android Studio.
3. Select "Import project (Gradle, Eclipse ADT, etc.)"
4. Navigate to the downloaded directory "android-components" and click "Open".
5. Keep all of the default options in the import wizard.

The project should be built after you open it. You cdan check its status in the Build Tool Window.

See also https://github.com/mozilla-mobile/android-components.
