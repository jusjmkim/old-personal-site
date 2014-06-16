---
layout: post
title: "Scraping Twitter Timestamps With Nokogiri"
date: 2014-06-14 23:40:00 -0400
comments: true
categories: "Flatiron&nbsp;School"
---
As test driven development becomes increasingly popular, the desire to test every facet of a piece of a code arises. My group found ourselves in this situation while trying to scrape from Twitter with a Ruby Gem called Nokogiri. However, when we ran our rspec test suite on our code (testing it with one of our twitters), we got this failure:

{% img center /images/scraping_twitter/tweet_string_rspec_failure_small.png 1500 2000 %}

These strings look exactly the same to us (the ends of the strings are also identical. I just took a screenshot of part of it too keep it all readable), and we should have been smart and basically considered this test a success. But, this project was more of an educational effort than anything else, and test-driven development dictates that we pass all our tests. Thus, we decided to look into this issue and find another way to test our code. After looking at the tweet's source code, we found this: 

{% img center /images/scraping_twitter/tweet_source_code.png %}

It seems that while the strings seem to be displaying the same, the actual output is still a Nokogiri XML output. If that was true, we couldn't go about validating the tweet directly. I wasn't sure what to do to test my code until I saw this:

{% img center /images/scraping_twitter/tweet_timestamp_source_code.png %}

Perhaps, we can confirm my code with each tweet's timestamp since every tweet, in theory, has a unique timestamp. After much Nokogiri work, we reached the result below, and it outputted a list of timestamps. (@student_twitters is simply an array of each student's twitter handle urls.)

{% img center /images/scraping_twitter/timestamp_method.png %}

It is important to note that while Nokogiri outputs all of these in square brackets, the output does not behave like an array at all. To be perfectly honest, I am not particularly well-versed in Nokogiri enough to explain why or definitively what is happening under the hood, but most array methods don't seem to work on the entire output. Rather, most methods used on the output only seem to target the first element. As shown in the rspec test suite below, we simply called the second element of the list via its index and asked if it included a timestamp I knew was there.

{% img center /images/scraping_twitter/timestamp_rspec.png %}

The code now passed its test suite! Furthermore, if one ever wanted to confirm the equality of twitter instances, on can do so as shown below.

{% img center /images/scraping_twitter/timestamp_equality.png %}

Nokogiri is fairly troublesome to use on large html documents, and knowing which css selectors to target and how to test for it may prove to be useful. I hope this post has proven to do just that for at least some of those who have bothered to read this far.