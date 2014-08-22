---
layout: post
title: "Installing Pindah"
date: 2014-07-10 09:17:11 -0400
comments: true
categories: 
---
http://jusjmkim.github.io/blog/2014/07/09/ruboto-vs-pindah-vs-rhodes-vs-sl4a/

<h2>Setup:</h2>
To set this up, you need JDK 6 or 7, any version of JRuby from 1.7.3 to 1.7.10, Mirah from 0.1.0 to 0.1.2, and Rake above 10.0.3. JDK should be installed through (http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html). If you are using RVM, JRuby should be installed through `rvm install jruby-1.7.10`. Then, to install Mirah, you have to use JRuby through `rvm use jruby-1.7.10` and then `gem install mirah-0.1.2`. Then, Rake can simply be gem installed via `gem install rake`.

As it turns out, if you visit the pindah github page (https://github.com/mirah/pindah/), at the time of this writing at least, the table under JRuby/Mirah Compatibility only goes up to `JRuby 1.7.10` and `Mirah 0.1.2`. This proved to be annoying to figure out because when I gem installed jruby, I got version 1.7.13, which I later found out was incompatible with Mirah 0.1.2. With RVM (which is what I use), you can easily switch jruby versions by doing `rvm use jruby-1.7.10`.

You must also use JDK 6 or 7, and at the time of this writing, JDK 8 is out. Thus, you have to downgrade JDK to the appropriate version to make this work, and OS X doesn't seem to provide an easy way to do this. Thus, adding the following lines of code to your bash_profile via `cd ~/.bash_profile` should set the default JDK version number to 7. (Remember to actually download JDK 7 from the Java website.)
<!-- more -->
```bash
function setjdk() {  
  if [ $# -ne 0 ]; then  
   removeFromPath '/System/Library/Frameworks/JavaVM.framework/Home/bin'  
   if [ -n "${JAVA_HOME+x}" ]; then  
    removeFromPath $JAVA_HOME/bin  
   fi  
   export JAVA_HOME=`/usr/libexec/java_home -v $@`  
   export PATH=$JAVA_HOME/bin:$PATH  
  fi  
 }  
 function removeFromPath() {  
  export PATH=$(echo $PATH | sed -E -e "s;:$1;;" -e "s;$1:?;;")  
 }
setjdk 1.7
```
To test if it works, in your bash, you should run the following line,
`mirah -e 'puts "Hello, Mirah!"'`

and have the output,
`Hello, Mirah!`

<h1>Additional Resources</h1>
http://www.drdobbs.com/jvm/language-of-the-month-mirah/229400307
http://thelogbox.com/android-programming-mirah-pindah/
http://pullmonkey.com/2011/11/13/hello-android-pindah-with-mirah-application/
http://confreaks.com/videos/196-rubyconf2009-ruby-mutants
