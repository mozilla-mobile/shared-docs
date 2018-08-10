# Android guide
This guide is designed to help you get started on Android and introduce you to some intermediate topics.

- [Getting started](#getting-started)
- [Staying informed](#staying-informed)
- [Intermediate topics](#intermediate-topics)

## Getting started
Assuming you already have some coding experience, Google's official [Developing Android Apps udacity course][udacity course] comes highly recommended by our team. After completing your first few lessons, you can try to working on our code base, continuing the course as necessary.

Once you have a little experience, the beginner's guides in the [official Android developer docs][devdocs] teach popular topics pretty well and are a good reference. However, they aren't very good at telling you where to go next (which is why we recommended the course). Note: the documentation on less popular topics are often missing information.

There are also many good Android tips and conference talks on YouTube.

## Staying informed
If you like staying up-to-date on the latest Android topics, members of our team recommend:
- Reading blogs
  - [Official Android developer blog](https://android-developers.googleblog.com/) (also has a newsletter)
- Subscribing to weekly newsletters
  - [Android weekly](https://androidweekly.net/)
  - [Android dev digest](https://www.androiddevdigest.com/)
- Listening to podcasts
  - [Fragmented](http://fragmentedpodcast.com/)
  - [Android Developers Backstage](https://androidbackstage.blogspot.com/)
- Visiting conferences (or watching their recordings)
  - Google IO
  - Android Developer Summit
  - Droidcon

## Intermediate topics
Comfortable with the basics? Here are a few of our favorite resources to get started on intermediate topics.
- [Android style tips](http://blog.danlew.net/2014/11/19/styles-on-android/) (circa 2014)

### Licenses ###
When adding a new license or updating an existing one, you need a list of libraries you're using so you can include their licenses. Most dependencies are included in the `build.gradla`e file, under `<dependencies>` but to get a complete list, you can run:

`./gradlew app:dependencies > dependency-report.txt`

This will include a tree of dependencies for all your build variants - usually you only need to look at the non-test Release variant in this list.

[udacity course]: https://www.udacity.com/course/new-android-fundamentals--ud851
[devdocs]: https://developer.android.com/docs/
