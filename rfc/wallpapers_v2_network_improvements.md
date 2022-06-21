* Start date: 2022-06-21
* RFC PR: #TODO

---

## Summary

The wallpapers feature was introduced on Android and iOS in v98 during Q1 2022. 
Due to late scope changes, a networking solution was quickly put together
in allow for delivering wallpapers from a remote source. As part of a
larger set of improvements planned for Q3 2022, it is intended to revisit
this implementation to create a more scalable version.

---

## Motivation

The original version of the networking solution consisted of
adding wallpaper image files to deeply nested directories which defined the properties
of the wallpaper. For example, an Android wallpaper might be found at:
```
<root>/mobile-wallpapers/android/<resolution>/<orientation>/<light/dark>/<wallpaper collection>/<wallpaper name>
```

This directory structure was confusing and difficult to manage. Copying several versions of a file to different locations
was painful, even when automated. Automation would require consistent file naming for each new set of wallpapers, which can
be hard to guarantee. 

Downloads were started automatically during app startup if a wallpaper was missing.

The files were also hosted by another Mozillian team, which may introduce complexity in terms of ownership or cost.

In general, we would like to achieve the following goals:

- it is easier for product, UX, and ENG to add new wallpapers
- it is possible to determine important metadata about a wallpaper, like its size or average color
- download is transparent to the user
- download is activated by the user
- require less bandwidth, if possible
- hosted in a more permanent, team-controlled location

---

## Guide-level explanation

Instead of relying on an (undocumented) convention for file paths, wallpaper metadata will be contained in a top-level JSON schema.
Using a well-known format will help discoverability, and JSON's extensiblility should allow for simpler long-term maintenance. 
It can also provide a more direct path to any required automation. This schema could define things like:

- Android file path(s)
- iOS file path(s)
- thumbnail path(s)
- average color (for text and background coloring purposes)
- collection grouping for things like seasonal promotions
- wallpaper expiration date
- wallpaper region availability

We will likely continue to ship some small number of wallpapers as part of our app binaries. This ensures that at least a few wallpapers are available for onboarding. We could also
just ship a few thumbnails and require users to download the wallpaper they are interested in once they reach the wallpaper settings page.

Additionally, including thumbnails will allow clients to keep download size relatively small. Thumbnails will need to follow the current eager downloading strategy
that wallpapers currently do. This will allow thumbnails to be decoupled from app releases, but they will still be visible when the settings page is open. The current suggestion is to
display some kind of action overlay above the thumbnails indicating that clicking them will cause a download.

---

## Drawbacks

- Maintenance burden of owning the hosting solution
