---
layout: post
title: "Scraping Twitter Timestamps With Nokogiri"
date: 2014-06-14 23:40:00 -0400
comments: true
categories: "Flatiron&nbsp;School"
---
As test driven development becomes increasingly popular, the desire to test every facet of a piece of a code arises. My group found ourselves in this situation while trying to scrape from Twitter with a Ruby Gem called Nokogiri. However, when we ran our rspec test suite on our code (testing it with one of our twitters), we got this failure:
<!-- more -->
```bash
expected: "New blog post about using abstraction and hashes to sort a music collection http://callahanchris.github.io/blog/2014/06/09/abstraction-and-music-library-sorting/ ... @aviflombaum"
got: "New blog post about using abstraction and hashes to sort a music collection http://callahanchris.github.io/blog/2014/06/09/abstraction-and-music-library-sorting/ ... @aviflombaum"
```

These strings look exactly the same to us (the ends of the strings are also identical. I just took a screenshot of part of it too keep it all readable), and we should have been smart and basically considered this test a success. But, this project was more of an educational effort than anything else, and test-driven development dictates that we pass all our tests. Thus, we decided to look into this issue and find another way to test our code. After looking at the tweet's source code, we found this: 

```html
<div class="ProfileTweet-contents">
  
  <p class="ProfileTweet-text js-tweet-text u-dir"
    
    dir="ltr">New blog post about using abstraction and hashes to sort a music collection 
    <a href="http://t.co/jRE2HgXYgi" rel="nofollow" dir="ltr" 
    data-expanded-url="http://callahanchris.github.io/blog/2014/06/09/abstraction-and-music-library-sorting/" 
    class="twitter-timeline-link" target="_blank" title="http://callahanchris.github.io/blog/2014/06/09/abstraction-and-music-library-sorting/" >
    <span class="tco-ellipsis"></span><span class="invisible">http://</span>
    <span class="js-display-url">callahanchris.github.io/blog/2014/06/0</span>
    <span class="invisible">9/abstraction-and-music-library-sorting/</span>
    <span class="tco-ellipsis"><span class="invisible">&nbsp;</span>…</span></a> 
    <a href="/aviflombaum" class="twitter-atreply pretty-link" dir="ltr" >
    <s>@</s><b>aviflombaum</b></a></p>
```

It seems that while the strings seem to be displaying the same, the actual output is still a Nokogiri XML output. If that was true, we couldn't go about validating the tweet directly. I wasn't sure what to do to test my code until I saw this:

```html
<span class="js-short-timestamp "
  data-time="1402347168"
  data-long-form="true">
  Jun 9
</span>
```

Perhaps, we can confirm my code with each tweet's timestamp since every tweet, in theory, has a unique timestamp. After much Nokogiri work, we reached the result below, and it outputted a list of timestamps. (@student_twitters is simply an array of each student's twitter handle urls.)

```ruby
def time_stamp
  time_stamps ||= @student_twitters.collect do |twitter_profile|
    page = Nokogiri::HTML(open("#{twitter_profile}"))
    time_stamp = page.search("span.js-short-timestamp").collect{|stamp| stamp.attribute("data-time").value}
  end
end
```

It is important to note that while Nokogiri outputs all of these in square brackets, the output does not behave like an array at all. To be perfectly honest, I am not particularly well-versed in Nokogiri enough to explain why or definitively what is happening under the hood, but most array methods don't seem to work on the entire output. Rather, most methods used on the output only seem to target the first element. As shown in the rspec test suite below, we simply called the second element of the list via its index and asked if it included a timestamp I knew was there.

```ruby
describe "#student_tweets" do
  it "contains tweets of students" do
    expect(twitter_scrape.time_stamp[1]).to include("1402606534")
  end
end
```

The code now passed its test suite! Furthermore, if one ever wanted to confirm the equality of twitter instances, on can do so as shown below.

```ruby
def ==(other_tweet)
  self.time_stamp == other_tweet.time_stamp
end
```

Nokogiri is fairly troublesome to use on large html documents, and knowing which css selectors to target and how to test for it may prove to be useful. I hope this post has proven to do just that for at least some of those who have bothered to read this far.