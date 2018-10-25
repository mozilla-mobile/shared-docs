# Android Accessibility Guide
Accessibility (or "a11y") is about making apps usable by everyone. Android developers need to pay particular attention to users with visual impairment, auditory impairment, and restricted motor skills. This guide is intended to get you started with making your Android app more accessible.

To identify how well the accessibility of your app is working, try it as a user! For example, try closing your eyes while using the TalkBack screen reader. You can also use [the Accessibility Scanner][scanner] for an automated analysis.

If you have questions, please ask!

## Introductory resources
The [official Android accessibility overview](https://developer.android.com/guide/topics/ui/accessibility/apps) is a great overview to common issues users may face and how you should address them as an Android developer. A good supplement, for visual impairment, is [this official Android Developers video](https://www.youtube.com/watch?v=1by5J7c5Vz4). This [presentation on accessibility](https://www.youtube.com/watch?v=UOr3mgqJU0A&feature=youtu.be&list=PLnVy79PaFHMUqqvwbjyKJZv1N8rzHOCBi) and [this podcast](https://androidbackstage.blogspot.com/2014/10/episode-14-accessibility.html) are also recommended by our developers.

Some general tips:
- Look through the accessibility preferences in the Developer Options: there are many features, such as visual simulations, to help you.
- If it is impossible to provide an intuitive, accessible user experience for your current UI, this is a design smell: a UI that is accessible tends to be the best experience for all users.
    - For example, a dialog with one option, like "Remove", that is dismissed by clicking outside the dialog, will be unintuitive to screen reader users. However, this dialog may be unintuitive to users who are unfamiliar with common software paradigms (i.e. tap outside to dismiss) too. A better dialog would be one with a "dismiss" option in addition to "remove"
- Avoid creating separate code paths and user experiences to address accessibility issues: in our experience, accessibility is not often tested so it's easy to break the experience if you forget to update one code path

## Screen reader tips
**TalkBack** is the default Android system screen reader: it's usually installed by default but you may need to install it from the Play Store. When testing, don't forget your headphones!

**VoiceView** is the default system screen reader on Amazon products: it is installed by default.

Some development tips:
- Don't try to override TalkBack's behavior outside of what is suggested in the docs: users expect the system to work consistently so overriding that behavior can be unintuitive.
    - Generally let the system handle focus changes: it's unintuitive when it jumps around.
- Overriding the accessibility APIs in code is a code smell: generally, you can make the changes you need using the methods recommended in the docs, which provides a more maintainable and intuitive experience to users. Also note the code APIs are unintuitive and not well documented.

## Automated testing
You can regularly use [the Accessibility Scanner][scanner] to get a cursory overview of how the accessibility of your app is doing.

Unfortunately, we don't have much automated testing experience outside of this. However, this [official documentation](https://developer.android.com/training/accessibility/testing#automated) seems like a good starting point. If you find out more, please share with the team and consider updating this doc!

[scanner]: https://support.google.com/accessibility/android/answer/6376570?hl=en
