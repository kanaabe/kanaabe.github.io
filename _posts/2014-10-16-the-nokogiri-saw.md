---
layout: post
title:  "The Nokogiri Saw"
date:   2014-10-16 16:25:21 -0400
categories: tutorial
---
In Japanese, the term “nokogiri” refers to this:

![Nokogiri Saw](http://hsto.org/storage/habraeffect/11/8d/118d003d546a1fa1e240e1cc4dfb4a61.jpg)

It’s a saw used for cutting wood, but instead of making the cut on the “push” like a traditional European saw, the Nokogiri saw cuts on the “pull”. Coming from a small [background](sites.google.com/site/digihumanlab/research) in Data Science, my brain lit up as soon as I was introduced to this magical gem.

## Define the Problem

After explaining to my boyfriend the concept of ‘scraping’, I asked him, “What do you want me to scrape for you?” “I want to know how to title my Reddit posts so it catches the most attention.” Great, problem defined.

## Spec It Out

Immediately I understand that solving this problem will take lots and lots of data and time. Therefore, the goal of this blog post is to lay out the foundation of a project that I can build on.

## Here's What I Know:

*   I want to scrape Reddit using Nokogiri
*   I want to retrieve the titles of each post
*   I want to use these titles and add them to some data structure I can iterate on
*   I want to find the most frequently used words
*   The Reddit RSS would be cool to use but I want to practice scraping.

## Discover Issues

One issue I encountered when trying to iterate through multiple pages is that the URL structure made no sense to me.

Page 1 - [http://www.reddit.com/](http://www.reddit.com/)

Page 2 - [http://www.reddit.com/?count=25&after=t3_2jg309](http://www.reddit.com/?count=25&after=t3_2jg309)

Page 3 - [http://www.reddit.com/?count=50&after=t3_2jg30w](http://www.reddit.com/?count=50&after=t3_2jg30w)

Page 4 - [http://www.reddit.com/?count=75&after=t3_2jgfto](http://www.reddit.com/?count=75&after=t3_2jgfto)

At first I figured that iterating through increments of 25 in the count parameter of the URL would work since each page contains 25 items.


{% highlight ruby %}
count = 0
  str = "http://www.reddit.com/?count="
  10.times do
    reddit << scrape_titles(str+(count+24).to_s)
    count = count + 25
  end
{% endhighlight %}


This did not work. What ended up happening was that duplicate titles appeared in my array. In fact, no matter what value I inserted for count, it showed me the same page. It was clear that getting a static URL for “Page 2 of Reddit’s Front Page” was not available. Based on the URL and HTML, the ‘after’ parameter was checking the ID of the post and creating content based on that. The ‘count’ param was irrelavent.

## Continue Anyway..

Instead of iterating through the front page titles, I decided to find the titles on the each of the Reddit subheading pages will do.

![Reddit](http://content.screencast.com/users/kabesailthru/folders/Jing/media/80a85640-8525-490e-ac5e-66b869adda92/00000166.png)

(Note: I excluded gilded, wiki, and promoted) Below is the code I have for my scraper class.


{% highlight ruby %}
class RedditScraper
  @@reddit = []
  PAGES = ["","/new/","/rising/","/controversial/","/top/"]

  def initialize_all_titles
    str = "http://www.reddit.com"
    PAGES.each do |page|
      @@reddit << scrape_titles(str+page)
    end

    @@reddit.uniq.flatten
  end

  def scrape_titles(str)
    doc = Nokogiri::HTML(open(str))
    arr=[]
    doc.css('a.title').each do |title|
      arr << title.text
    end
    arr
  end

end
{% endhighlight %}

Running RedditScraper.new.initialize_all_titles returns an Array with all my title names. Awesome! Here is a sample of my output so far

![Results](http://content.screencast.com/users/kabesailthru/folders/Jing/media/4ce3c544-0f71-4bec-b463-7e0a19b0f55c/00000168.png)

Next I need to analyze this data. What I really want to do is to find the frequency of each of the words to see “what’s trending” right now. I created a class called RedditAnalyzer which allows me to do this. Lets iterate through our titles array, graciously given to us by RedditScraper, find individual words, and keep a frequency count each time I come across this word.


{% highlight ruby %}
class RedditAnalyzer
  @@frequency = {}

  def call
    scraper = RedditScraper.new.initialize_all_titles
    add(scraper)
    #binding.pry
  end

  def add(arr)
    arr.each do |title|
      title.downcase.split(" ").each do |word|
        word.gsub(/[,.\[\]'?!-\"]/, "")
        if @@frequency[word]
          @@frequency[word] = @@frequency[word] + 1
        else
          @@frequency[word] = 1
        end
      end
    end

  end
end
{% endhighlight %}

Two more functions I decided to add are below. delete_common is called from top_20 and removes the 100 most common words in the English language. The top_20 function prints out the top 20 most frequently used words.


{% highlight ruby %}
def top_20
    delete_common
    sorted = @@frequency.sort_by {|k,v| -v}
    sorted.each_with_index do |word,ind|
      puts "#{word[0]} with frequency #{word[1]}" if ind <=19
    end
  end

  def delete_common
    text = []
    File.read("resources/common_words.txt").each_line do |line|
      text << line.chop
    end
    @@frequency.each do |word,v|
      if text.include?(word)
        @@frequency.delete(word)
      end
    end
  end
{% endhighlight %}

## AND FINALLY..THE TOP 20 MOST FREQUENT WORDS USED IN A TITLE ON REDDIT AT 3:41AM ON 10/17:

i with frequency 18

not with frequency 10

til with frequency 6

‘-’ with frequency 5

why with frequency 5

using with frequency 5

just with frequency 4

man with frequency 4

ebola with frequency 4

good with frequency 4

best with frequency 4

only with frequency 4

18 with frequency 3

while with frequency 3

million with frequency 3

travel with frequency 3

guy with frequency 3

sick with frequency 3

don’t with frequency 3

eli5: with frequency 3

## “TIL: WHY 18 MILLION DON’T TRAVEL WHILE MAN IS SICK WITH EBOLA”

Maybe I should create some bots next…

Full repo: [https://github.com/kanaabe/scraping_reddit](https://github.com/kanaabe/scraping_reddit)

## TODO LIST

*   get rid of that ‘-’ word
*   add visualization using another Ruby gem
*   possibly add more ‘common words’
*   refactor some methods from above, I was being hasty.