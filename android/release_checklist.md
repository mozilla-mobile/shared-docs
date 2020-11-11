# Android Development/QA Release Checklist

## Summary

This is a list of important items to consider for developers and QA before releasing an Android app to a store.

## General

[ ] Run a full app lint check and go over the results in detail for anything that might need to be fixed.

## State Handling

### Handling UI Changes

[ ] Verify UI state is maintained properly on screen rotation for each screen of the app.
[ ] Check both portrait and landscape modes to verify that UI elements appear onscreen for each screen of the app in both configurations.
[ ] See what happens when Android 7.0 multi-window/split-screen mode is enabled (long-press the app icon in recent tasks mode). Simply being able to use the app and interact should be enough.
[ ] Test on the major tablet sizes (7" and 10") in portrait and landscape.
[ ] Test on a minimum specs device using the lowest supported version of Android and a small screen and memory size to verify that the app can still load and perform basic functions. Make sure the UI elements appear correctly and fit onscreen without overlap. Features like tinting drawables often does not function as well under older Android versions.
[ ] Since Android Intel devices are uncommon these days and run very different native code, it's valuable to try each screen of the app on a Chromebook and verify that nothing seems broken.
[ ] Switch to Don't Keep Activities Mode under Developer Settings. Verify that each screen of the app maintains its state when minimized and restored.
[ ] Ensure that all views have IDs to be used by the OS for persisting instance state and by QA to create automated UI tests.
[ ] If dark mode or private mode themes are available, ensure that all UI elements and colors can clearly be seen in each mode.

### Handling Network Changes

[ ] See how the app functions when started in airplane mode.
[ ] Verify that the app does not crash on cold start when no internet is available using the current connection. This is different from testing in airplane mode.

### Handling Race Conditions

[ ] Run RoboTest or the Monkey application exerciser to verify that UI race conditions are handled. These days, this is also typically handled by Google's pre-launch report, but it doesn't hurt to try it yourself.

### Handling All Entry Points

[ ] Verify that the app can be launched safely using all possible intent filters. If the app can be started by a notification, ensure that nothing bad happens if the app is already open to various screens when you tap that notification.
[ ] Verify that launching the app from both recents and the launcher icon returns you to where you left off in the app. Sometimes application launch modes can mess with this.

## Internationalization

[ ] Ensure the latest strings have been imported from translators.
[ ] Run pseudolocale testing to verify that locales with longer text will not have overlapping or cut off text, that no text is hard-coded incorrectly, and that right-to-left locales correctly appear with reversed layouts.
[ ] Run FastLane screengrabs for all supported locales and verify that no locale crashes or looks seriously incorrect.

## Accessibility

[ ] Test using minimum and maximum font scaling settings in the OS. Again, check for overlapping or cut off text. Verify that all text in the app uses sp units, not dp or px.
[ ] Have someone test using the app with accessibility devices, such as a screen reader. Ensure that items relevant to the page have a reasonable content description and that irrelevant items, like a logo that cannot be interacted with, set importantForAccessibility="no".
[ ] Run the accessibility scanner against each screen of the app to verify whether common mistakes were made, such as using text and button targets which are too small or colors which do not contrast enough for people with color-blindness. Better yet, add automated AccessibilityChecks (https://developer.android.com/guide/topics/ui/accessibility/testing) to automated UI tests for each screen.

## Performance

[ ] Use Strict Mode (https://developer.android.com/reference/android/os/StrictMode) to help verify that the main/UI thread is not being blocked unnecessarily. Use Nimbledroid.com to check for performance issues on cold starts.
