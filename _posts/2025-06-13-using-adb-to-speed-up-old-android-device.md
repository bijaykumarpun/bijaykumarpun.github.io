---
layout: post
title: "Using adb to speed up old Android device"
date: 2025-06-12 12:00:00
description: "Disabling packages that aren't needed on a test device"
---

#### Background

I was contemplating on buying a new Android device for development & testing purposes because the old ones I had were lagging pretty bad [thanks to Samsung]. However, I also didn't want to spend another fortune on a flagship phone. One alternative I had was to root the phone or install a custom ROM - but I wasn't too sure if that would solve the issue; this would also introduce another variable in testing that I just didn't have the capacity for.

After some fiddling around, I came across this idea of using `adb` to disable apps that were not needed on the phone and, to my grand surprise, the result was super impressive.

#### Steps:

##### 1. Enable USB debugging on the Phone & connect to the PC
##### 2. Ask ChatGPT on the list of packages that aren't needed on your Android device model. That should give out a list like this:
```
# For Samsung Galaxy M02
com.sec.android.app.sbrowser.lite           # Samsung Internet Lite
com.samsung.android.app.galaxyfinder        # Finder/Search on Samsung
com.samsung.android.smartswitchassistant    # Smart Switch
com.sec.android.app.billing                 # Samsung billing client
com.samsung.android.app.settings.bixby      # Bixby settings
com.samsung.android.privateshare            # Private share (rarely used)
com.sec.android.daemonapp                   # Weather daemon
com.sec.android.easyMover.Agent             # Data transfer
com.sec.android.gallery3d                   # Samsung Gallery (disable if using Google Photos)
com.sec.android.app.myfiles                 # My Files app (can be replaced)
com.samsung.android.messaging               # Samsung Messages (if using Google Messages)
com.samsung.android.app.contacts            # Samsung Contacts (if using Google Contacts)
com.google.android.youtube                  # YouTube (can be reinstalled later)
com.google.android.gm                       # Gmail (if using other mail app)
com.google.android.apps.tachyon             # Google Duo/Meet
com.microsoft.skydrive                      # OneDrive
com.facebook.services
com.facebook.system
com.facebook.appmanager                     # Facebook bloatware
com.samsung.android.app.soundpicker         # Sound picker (not essential)
com.samsung.android.forest                  # Samsung's forest campaign app
com.sec.android.app.clockpackage            # Samsung Clock (if replaced)
com.google.android.apps.maps                # Google Maps (disable if unused)
com.samsung.android.app.updatecenter        # App update center
com.sec.android.app.fm                      # FM Radio
com.sec.android.app.personalization         # Theme & wallpaper store
com.samsung.android.mdx.quickboard          # Samsung Continuity clipboard
com.sec.android.widgetapp.webmanual         # Samsung user guide
com.sec.android.app.dressroom               # Themes/Dressroom app
com.sec.mygalaxy.NEBangS                    # My Galaxy bloatware
com.wsomacp                                 # Unknown carrier-related
com.samsung.android.bluelightfilter         # Night light filter
com.sec.imslogger                           # IMS logger (VoLTE debug tool)
com.samsung.android.aircommandmanager       # Air Command (for S Pen — M02 doesn’t have it)
com.sec.bcservice                           # Knox
com.samsung.klmsagent                       # Knox Key Agent
com.android.egg                             # Android Easter egg
com.aura.oobe.samsung                       # Aura bloatware
```

##### 3. Create a `.sh` file and save it on PC

```
# disable-packages.sh
#!/bin/bash

# Re-enable (reinstall) Samsung and third-party bloatware packages

packages=(
  com.samsung.android.app.galaxyfinder
  com.samsung.android.smartswitchassistant
  com.samsung.android.calendar
  com.sec.android.app.sbrowser.lite
  com.samsung.android.messaging
  com.samsung.android.MtpApplication
  com.sec.android.app.myfiles
  com.samsung.android.smartcallprovider
  com.samsung.android.app.contacts
  com.samsung.android.biometrics.app.setting
  com.samsung.android.app.clockpack
  com.samsung.android.app.updatecenter
  com.samsung.android.app.omcagent
  com.sec.android.app.fm
  com.facebook.katana
  com.facebook.services
  com.facebook.system
  com.facebook.appmanager
  com.microsoft.skydrive
  com.hiya.star
  com.sec.android.easyMover.Agent
  com.samsung.klmsagent
  com.samsung.android.privateshare
  com.sec.android.gallery3d
  com.sec.android.daemonapp
  com.sec.android.app.soundalive
  com.sec.android.app.billing
  com.sec.android.app.SecSetupWizard
  com.aura.oobe.samsung
  com.sec.android.app.ringtoneBR
  com.samsung.android.shortcutbackupservice
  com.sec.android.app.personalization
  com.samsung.android.app.settings.bixby
  com.samsung.android.mdx.quickboard
  com.sec.android.app.samsungapps
  com.samsung.android.app.dressroom
  com.samsung.app.newtrim
  com.samsung.android.lool
  com.sec.mygalaxy.NEBangS
  com.samsung.android.forest
  com.samsung.safetyinformation
  com.google.android.youtube
  com.google.android.gm
  com.google.android.apps.maps
  com.google.android.apps.tachyon
  com.google.android.projection.gearhead
  com.google.android.apps.turbo
  com.android.egg
)

for package in "${packages[@]}"
do
  echo "Disabling $package..."
  adb shell pm uninstall --user 0 "$package"
done

echo "Done. Packages disabled."

```

##### 4. Make the script executable

`sudo chmod +x disable-packages.sh`

##### 5. Execute

`./disable-package.sh`

Point to note:
- This will disable most of the apps so it's important to properly check what packages are being disabled
- To re-enable, use `adb shell cmd package install-existing "$package"`

---