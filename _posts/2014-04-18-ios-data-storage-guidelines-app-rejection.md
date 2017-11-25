---
layout: post
title: "iOS Data Storage GuideLines - App Rejection"
modified: 2014-04-18 09:58:54 -0400
tags: [ios, appstore, datastorage, icloud]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true 
---

## Binary Rejected  

### Reasons for Rejection:

> 2.23 Apps must follow the iOS Data Storage Guidelines or they will be rejected
In particular, we found that on launch and/or content download, your app
stores 41.6 MB. To check how much data your app is storing:


- Install and launch your app
- Go to Settings > iCloud > Storage & Backup > Manage Storage 
- If necessary, tap "Show all apps"
- Check your app's storage

### Solution

The iOS Data Storage Guidelines indicate that only content that the user
creates using your app, e.g., documents, new files, edits, etc., should
be backed up by iCloud.

Temporary files used by your app should only be stored in the /tmp directory; please remember to delete the files stored in this location when the user exits the app.

But we usually kept the persisting images or assets for offline use in Documents directory or  sub folder created under Documents Directory. That should be marked with "do not back up" attribute. 

{% highlight objc %}
- (BOOL)addSkipBackupAttributeToItemAtURL:(NSURL *)URL
{
    if (&NSURLIsExcludedFromBackupKey == nil) { // iOS <= 5.0.1
        const char* filePath = [[URL path] fileSystemRepresentation];
        
        const char* attrName = "com.apple.MobileBackup";
        u_int8_t attrValue = 1;
        
        int result = setxattr(filePath, attrName, &attrValue, sizeof(attrValue), 0, 0);
        return result == 0;
    } else { // iOS >= 5.1
        NSError *error = nil;
        [URL setResourceValue:[NSNumber numberWithBool:YES] forKey:NSURLIsExcludedFromBackupKey error:&error];
        return error == nil;
    }
}
{% endhighlight %}

It is necessary to revise your app to meet the requirements of the iOS Data Storage Guidelines.