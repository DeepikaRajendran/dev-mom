---
layout: post
title: "Decompile an Android App"
modified: 2014-04-14 22:22:45 -0400
tags: [android, mobile development,decompile]
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: true
---

1. Download apk from any source
2. Download Dex2jar tool
3. Execute following command to extract <APKNAME>.apk in form *smali files: d2j-dex2jar.bat <APKNAME>.apk
4. Download JD-GUI and execute following command: jd-gui.exe <APKNAME>-dex2jar.jar  .  By executing the command, you will get source code of that APK which could be viewed and studied