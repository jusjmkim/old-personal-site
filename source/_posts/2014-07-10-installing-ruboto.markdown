---
layout: post
title: "Installing Ruboto"
date: 2014-07-10 09:17:06 -0400
comments: true
categories: 
---
http://jusjmkim.github.io/blog/2014/07/09/ruboto-vs-pindah-vs-rhodes-vs-sl4a/
<h2>Setup:</h2>
First of all, you should gem install ruboto to get started. Then, you should install your JDK or Java Development Kit. The link to JDK 8, the latest at the time of this writing is available here: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html. 

To install ant (assuming you have homebrew installed), do the following:
`brew install ant`

Then, run the following command to run the rest of the setup.
`ruboto setup`
The android developer website has a great section on how to install the android sdk, which you also need, to get ruboto working. http://developer.android.com/tools/help/sdk-manager.html

<!-- more -->

When they prompt you for your configuration script, type in: .bash_profile because that is one of the files that configures all of your bash settings, such as your environment variables. In this case, Ruboto simply wants to add the relevant directories to your PATH.

<h1>Additional Resources</h1>
http://www.sitepoint.com/ruboto-rubys-and-androids-first-born/
http://ruboto.org/
http://rubylearning.com/blog/ruboto-quick-start/ (also helps set up an Android Virtual Device)
https://www.youtube.com/watch?v=3074P4juuXs