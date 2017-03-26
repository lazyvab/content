---
layout: post
title: "Requestly release process"
modified:
categories: developers
sample: false
excerpt: "Steps for building Requestly to deploy on Chrome Store"
tags: []
date: 2016-05-10T18:03:30 +05:30
comments: true
share: true
---

## Steps

- Checkout master branch and fetch it `git checkout master && git pull origin master`
- Checkout `production` branch - `git checkout production && git pull origin production`
- Merge master branch to it - `git merge master`
- Run Unit tests - `grunt test`
- Update version number in `Shared.js, manifest_chrome.json, mainfest_firefox.json, package.json, Gruntfile.json`
- Disable Logger in logger.js
- Run build command - `grunt release-chrome`
- Upload the build to [Chrome Store](https://chrome.google.com/webstore/developer/dashboard)
- Delete the earliest build. We want to keep only 3 previous builds.
- Run command - `./release-firefox.sh`
- Copy the new artifact to static-content repo (We currently host firefox builds on firebase)
- Recopy copied artifact as requestly-latest.xpi (This is linked on requestly home page and all other pages)
- Update updates.json inside static-content directory
- Enable Logger in logger.js
- Commit the files - `git add . && git commit -m "Requestly va.b.c released"`
- Push to production branch - `git push origin production`
- Add tag - `git tag -a va.b.c -m Requestly va.b. released`
- Push the tags - `git push --tags origin`
- Merge to master - `git checkout master && git merge production`
- Push master - `git push origin master`

## Notes

1. Requestly uses `grunt-zipup` to create a zip file of source code. 
This tool only works on Unix or Mac So requestly's zip can only be created on Linux/Mac OS.
