---
layout: post
title: "Ruboto vs Pindah vs Rhodes vs SL4A"
date: 2014-07-09 23:30:15 -0400
comments: true
categories: 
---
This blog post is mainly a compilation of my googling Ruboto, Pindah, Rhodes, and SL4A when deciding which platform to use for android development. None of this information is my own opinion (except perhaps the conclusion in which I choose one to learn). I chose these four technologies because they are all platforms on which to develop native android apps with Ruby. I will be discussing the pros and cons of each of these, with particular emphasis on Ruboto and Pindah.

<h1>Ruboto</h1>
Ruboto is a framework to allow android developers to use Ruby in order to develop apps. Java source files are compiled and packed together with JRuby JARs to give you access to the Android API. You can then run your custom Ruby script with this API to create your Android app. At the time of this writing, Ruboto is gaining a lot of popularity.

http://jusjmkim.github.io/blog/2014/07/10/installing-ruboto/

<h2>Pros:</h2>
<ul>
  <li>Does not need to recompile the entire application</li>
  <li>Has IRB built-in</li>
  <li>Good documentation</li>
</ul>

<h2>Cons:</h2>
<ul>
  <li>Has a large runtime library (simple Hello World app is several MB large)</li>
  <li>Subjected to JRuby initialization costs. Start up for app is several seconds long.</li>
</ul>
<!-- more -->
<h1>Pindah</h1>
Pindah is definitely an interesting piece of technology as it utilizes a new language called Mirah. It was developed by the same person who made JRuby, and he made it to seem extremely similar to Ruby. (The differences between the two are listed here: https://github.com/mirah/mirah/wiki/Differences-from-Ruby). Mirah is static typed and runs on JVM. While developers are a little wary of how young Mirah is, there is a lot of excitement over its compiling to JVM bytecode.

http://jusjmkim.github.io/blog/2014/07/10/installing-pindah/

<h2>Pros:</h2>
<ul>
  <li>Ends up as JVM bytecode</li>
  <li>Runs as fast as Java.</li>
  <li>Similar syntax to Ruby</li>
  <li>No runtime library</li>
</ul>

<h2>Cons:</h2>
<ul>
  <li>Still extremely new</li>
  <li>Not as much documentation</li>
  <li>Pindah is infrequently updated</li>
</ul>

<h1>Rhodes</h1>
The Rhodes Framework is more formally known as the RhoMobile Suite, and it is an open-source framework created by Motorola. It compiles down to Ruby bytecode and does not use the Dalvik JVM. It is very popular among large companies because it supports all major smartphone platforms. It structured similarly to Rails in its use of Object Relational Mapping (ORM) and the Model-View-Controller (MVC) framework. Note that Rhodes only supports up to Ruby 1.9.3 at the time of this writing.

To install Rhodes: http://docs.rhomobile.com/en/2.2.0/rhodes/tutorial. Note that it does not support (at the time of this writing) android-ndk r9d. r8d worked for me. Use this link to learn to brew install the specific version (http://stackoverflow.com/questions/3987683/homebrew-install-specific-version-of-formula). I recommend reading all the links I provided because they have all proven to be extremely helpful. While I provided installation posts to Pindah and Ruboto, I will not for Rhodes because my installation process was extremely convoluted and confusing, and I can't remember how I did it exactly (or really which steps actually worked). I will note, though, that I could not rake run:android on Terminal, but I got the Android Virtual Device working on RhoStudio, so that's probably the best way to go.

<h2>Pros:</h2>
<ul>
  <li>Cross-platform (supports all major smartphone platforms)</li>
  <li>Can compile iOS apps on Windows</li>
  <li>Uses HTML</li>
  <li>Supports synchronized offline data</li>
  <li>Has an IDE(Rhostudio)</li>
  <li>Structured very similarly to Rails (e.g. Has ORMs and an MVC framework)</li>
</ul>

<h2>Cons:</h2>
<ul>
  <li>There is the temptation to use the same code base for all platforms</li>
</ul>

<h1>SL4A</h1>
SL4A is a simple abbreviation for Scripting Layer for Android, which was previously called Android Scripting Environment (ASE). It is a great way to write scripts for Android, but it is not meant for production use, especially because the Android device needs SL4A installed to run the scripts.

<h2>Pros:</h2>
<ul>
  <li>Has a simplified interface</li>
  <li>Supports many languages (e.g. Python, Perl, Ruby, Javascript)</li>
  <li>Great for scripting</li>
</ul>

<h2>Cons:</h2>
<ul>
  <li>Still alpha software</li>
  <li>Is meant for developers</li>
  <li>Android needs SL4A installed to run scripts</li>
</ul>

<h1>Conclusion</h1>

I personally decided to go with Rhodes because my background is primarily in Rails (as are most Ruby developers'), so the learning curve should be much nicer. It is widely adopted and versatile in its platform support. As a second choice, I would have probably gone with Pindah because of its sheer speed and small fingerprint. I will probably write another blog post about my experience with Rhodes, so stay tuned!

<h1>Additional Resources</h1>
Ruboto<br>
http://www.sitepoint.com/ruboto-rubys-and-androids-first-born/<br>
http://ruboto.org/<br>
http://rubylearning.com/blog/ruboto-quick-start/ (also helps set up an Android Virtual Device)
https://www.youtube.com/watch?v=3074P4juuXs<br>

Mirah<br>
http://www.drdobbs.com/jvm/language-of-the-month-mirah/229400307<br>
http://thelogbox.com/android-programming-mirah-pindah/<br>
http://pullmonkey.com/2011/11/13/hello-android-pindah-with-mirah-application/<br>
http://confreaks.com/videos/196-rubyconf2009-ruby-mutants<br>

Rhodes<br>
https://www.youtube.com/watch?v=asXhmWXcxBY<br>
http://docs.rhomobile.com/en/2.2.0/rhodes/build<br>
http://rubylearning.com/blog/2010/12/07/want-to-build-a-mobile-app-on-an-android%E2%84%A2-phone-with-rhodes/<br>
http://www.slideshare.net/adamblum/using-ruby-in-android-development<br>
http://devproconnections.com/development/product-review-rhomobiles-rhombus-smartphone-app-development-product-suite<br>
http://docs.rhomobile.com/en/2.2.0/rhodes/install<br>
http://techleap.blogspot.com/2011/04/how-to-make-your-first-application.html<br>
https://gist.github.com/nicksoto/2879726<br>
https://github.com/rhomobile/rhodes/issues/191<br>

SL4A<br>
https://code.google.com/p/android-scripting/wiki/FAQ<br>

Miscellaneous<br>
https://groups.google.com/forum/#!topic/dallasrb/LOq7uVh_sic

