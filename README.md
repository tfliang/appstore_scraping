# Appstore scraping

Working on a project for better awareness of air quality, I was interested in knowing what the main apps related to this field
were like. I'd like to (partially) answer the following questions:
* What apps are there?
* What are their main features?
* How are they rated?
* What are users looking for when using those apps?
* What expectations are not currently met?
* How do these apps work? Is there a classification for such apps?

After some research, it seems that Scrapy (https://doc.scrapy.org/en/latest/index.html) should help me scrape the data needed for my analysis.

Basically, Scrapy allows for gently scraping the web, which is what I'm intended here, by creating spiders and sending them out to crawl the app stores.

---
For the time being, I've been busy getting a better understanding of:
*  How to navigate html response using css attributes (when the response is in html).
    - How to deal with multiple classes in css tags to access the right level of data
*  How to "translate" unicode text with '\r\n\t' and leading and trailing whitespaces
    - Used the .translate() function with the following dictionary: trans_table = {ord(c): None for c in u'\r\n\t'}
    - Used the .strip() function to get rid of leading and trailing whitespaces
* Understand dynamic requests: when the URL has a '#', the server does not care about what's after this symbol. The client (web browser) deals with it. Then, I went to the Developer's tools to find out where I could identify the "real" url I would need for scraping. Learned about cURL!
    - How to transform the cURL of into a request that can be handled by Scrapy (done manually at first, and discovered it can also be done using https://michael-shub.github.io/curl2scrapy/: thank you!!)
* How to build a spider where the requests have headers and deal with responses in JSON format
    - How to easily visualize the tree structure of a JSON format (thanks to: https://jsonformatter.org/json-viewer)
    - How to decode parameters from a URL in order to tidy up the code (thanks to: https://meyerweb.com/eric/tools/dencoder/)

---
Next steps:
* Review the settings of my spiders to ensure gentle scraping (so far, I've been selecting pages with limited amount of data to scrape on purpose)
* Build two distinct spiders:
    1. One to collect app features and description across a range of apps
    2. One to collect reviews for a specific app
* Identify relevant apps (so far, couldn't find an app search menu outside the appstore app...)
* Investigate "live" apps: Are apps still maintained? Downloaded?
* Have a look at the review texts (strange feeling when reading some of them)
* Investigate how to automate data extraction from text reviews
