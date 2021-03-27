# How to fix widevine and ffmpeg problems in Opera-Browser (Deb) version on Linux

## Prerequisites
  - Chromium-ffmpeg - [here](https://snapcraft.io/chromium-ffmpeg).
  - Google Chrome -  [here](https://www.google.pt/intl/pt-PT/chrome/). #optional
### Chromium-ffmpeg (deb) version
  For those who prefer .deb versions, chromium is available for an unofficial [ppa](https://launchpad.net/~xalt7x/+archive/ubuntu/chromium-deb-vaapi).
  
## Widevine

### Solution One
  You can just install Google Chrome and keep it as a "dependency" on Opera. In this case, Opera's default configuration would already pull the WidevineCdm directory directly from Chrome, that is, its configuration would not be necessary.
  
### Solution Two
  The WidevineCdm directory is inside your user's ".config / opera" folder, just not being pointed in the widevinecdm configuration file. Your solution would be to just point this directory in the file.
  
The WidevineCdm folder can be found by these paths:
```
  |-> /
    |-> home
      |-> your-username
        |-> .config
          |-> opera
            |-> WidevineCdm
              |-> 4.10.1610.0 <- our configuration file should point directly to this folder
```
In case the WidevineCdm directory is not present in the opera folder, enter the address opera://components and try to update all the components in the list.

The widevinecdm configuration file can be found by following the path:
```
  |-> /
    |-> usr
      |-> lib
        |-> x86_64-linux-gnu
          |-> opera
            |-> resources
              |-> widevine_config.json <- file to be edited

```
you can just replace the contents of the file with the widevinecdm directory, leaving you like this:
```json
[
    "/home/your-username/.config/opera/WidevineCdm/4.10.1610.0"
]
```
or add the directory at the end of the file, like this:
```json
[
  "/opt/google/chrome/WidevineCdm",
  "/opt/google/chrome-beta/WidevineCdm",
  "/opt/google/chrome-unstable/WidevineCdm",
  "/home/you-username/.config/opera/WidevineCdm/4.10.1610.0"
]
```
If the WidevineCdm folder is not found within /home/your-user/.config/opera, access the [opera://components](opera://components) page and click on the "Check for Update" button for each component.

## FFmpeg
  In the snap version the files can be found like this:
```
   |-> /
     |-> snap
       |-> chromium-ffmpeg
         |-> current
           |-> chromium-ffmpeg-*
             |-> chromium-ffmpeg
               |-> libffmpeg.so
```
#### Or
  For those who chose the (deb) version, the files can be found as follows:
```
  |-> /
    |-> usr
      |-> lib
        |-> chromium-browser
          |-> libffmpeg.so
```
## Configuring ffmpeg (Not needed for the (deb) version of chromium)
  The file to be modified is at:
```
  |-> /
    |-> usr
      |-> lib
        |-> x86_64-linux-gnu
          |-> opera
            |-> resources
              |-> ffmpeg_preload_config.json
```
  We will only inform the path of the libffmpeg.so files, it will change depending on the installed version of Chromium-ffmpeg as we have already seen.
  The original content of the files would be this:
```json
[
  "../../../../chromium-ffmpeg/libffmpeg.so",
  "/usr/lib/chromium-browser/libffmpeg.so",
  "/usr/lib/chromium-browser/libs/libffmpeg.so"
]
```
  After the added path it would look like this:
```json
[
  "../../../../chromium-ffmpeg/libffmpeg.so",
  "/usr/lib/chromium-browser/libffmpeg.so",
  "/usr/lib/chromium-browser/libs/libffmpeg.so",
  "/snap/chromium-ffmpeg/current/chromium-ffmpeg-95241/chromium-ffmpeg/libffmpeg.so"
]
```
  A list of versions of chromium-ffmpeg (snap):
  ```
    |-> /
     |-> snap
       |-> chromium-ffmpeg
         |-> current
          |-> chromium-ffmpeg-91124
          |-> chromium-ffmpeg-91696
          |-> chromium-ffmpeg-92142
          |-> chromium-ffmpeg-92393
          |-> chromium-ffmpeg-92972
          |-> chromium-ffmpeg-93464
          |-> chromium-ffmpeg-94142
          |-> chromium-ffmpeg-95241
          |-> meta
          |-> snap
  ```
  All libffmpeg.so files found in the chromium-ffmpeg- * folders work, feel free to shrink anyone!
  
### Finishing
  After all this, save the edited files and restart your opera so that all modifications are effective.
  
### Obs
  Have a copy of the edited files, because with each new update of the opera these files are reset to their original version. If this happens just edit the files again or paste the copies of the files already edited.
