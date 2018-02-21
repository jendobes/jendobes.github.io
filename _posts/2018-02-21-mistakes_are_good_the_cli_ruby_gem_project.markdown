---
layout: post
title:      "Mistakes are good: the CLI Ruby Gem Project"
date:       2018-02-21 19:15:15 +0000
permalink:  mistakes_are_good_the_cli_ruby_gem_project
---


Daily Phrases ruby gem: my first coding project that is 100% really truly mine. I love it and it is my baby. And just like an infant it drove me insane and I sometimes secretly wished I hadn’t created it in the first place. 

My gem scrapes web pages to provide a daily phrase in 15 different languages along with an English translation. This seemed simple enough, and in the beginning it was. I spent two blissful days writing the structure and CLI of my gem, using stubs as the output. I was feeling confident and accomplished right up to building my scraper method. Then I was just flat out angry. NOTHING worked. 

I originally tried using Nokogiri with CSS class selectors to scrape the phrase and translation text. No matter what I tried, Nokogiri consistently returned the dreaded => [ ]. After a day of table pounding and screaming “WHY!?” at my laptop, I realized Nokogiri wasn’t able to access the code I wanted since it’s wrapped in an iframe widget filled with JavaScript rendered content. I needed to download a few gems such as Watir, Capybara and Chromedriver to create a headless browser that would access and load the JavaScript content for Nokogiri to scrape.

Between figuring out what exactly my problem was and coming up with a solution, I had passed 3 days of total and complete frustration, for which I am very grateful.
I understand more about the mechanics of gems and web code than I ever would have if my initial Nokogiri scrape was successful. Here’s a quick overview of how my scraper method accesses content:

1. create the browser variable using Watir and Chromedriver. Watir manipulates the browser after Chromedriver accesses the Chrome binary and launces a browser window.
2. browser goes to the specified URL
3. switch_to.frame allows Watir to access the nested iframe, specified by the iframe index. The iframe I needed was the only one on the page and therefore had an index of 0
4. By accessing the iframe widget via Watir, the JavaScript rendered content is loaded and appears in the HTML. If Nokogiri tried to scrape the widget's URL without Watir, it would only be able to access the source code which is devoid of the JavaScript content.
5. Nokogiri  parses the browser's HTML, selects the desired JavaScript content, and returns the phrase and translation.


```
    browser = Watir::Browser.new :chrome
    browser.goto "https://www.transparent.com/word-of-the-day/today/#{input}.html"
    browser.driver.switch_to.frame(0)
    doc = Nokogiri::HTML.parse(browser.html)

    phrase_scrape = doc.css("p.js-wotd-fnphrase").text
    translation_scrape = doc.css("p.js-wotd-enphrase").text
    browser.driver.quit
```
