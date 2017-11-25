---
layout: post
title: "Detect Shake Gesture in iOS"
modified: 2014-04-14 22:22:45 -0400
tags: [android, mobile development,decompile]
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: true
---

In this tutorial we will see how to detect a shake gesture in iOS devices.

Steps:

Project Creation:

1. Open XCode and create a new Single View application

2. Fill out "Product Name", "Organization" and other details

3. Select "StoryBoard" and "ARC Enabled" checkboxes

4. The storyboard is created with default "ViewController" class.


Responder

ViewController should be first responder to identify the shake gesture. To receive motion events, designate responder object as first responder. Below is the code snippet to set the view controller as "first responder".

{% highlight objc %}

-(void)viewDidAppear:(BOOL)animated{
   [self becomeFirstResponder];
}

-(BOOL)canBecomeFirstResponder{
   return YES;
}

{% endhighlight %}

Implementing motion handing events - This code detects whether a shake has occurred in the motionEnded:withEvent: method, and if it has,  shows the alert.

{% highlight objc %}

-(void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event{
    if(motion == UIEventSubtypeMotionShake){
         UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:@"Shake Detector" message:@"Shake is detected" delegate:nil cancelButtonTitle:@"Ok" otherButtonTitles: nil];
         [alertView show];
    }
}

{% endhighlight %}

The source code will be available here