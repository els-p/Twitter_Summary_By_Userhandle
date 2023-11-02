# Twitter_Summary_By_Userhandle
Aggregate tweets from multiple users and get a concise overview of the latest sentiments and ideas circulating within the crypto space.

## Problem statement
The crypto space is hyper dynamic. Staying updated with the constant developments can be challenging. 

## Goal
To write a code that can automate the aggregation of latest posts from a handful of super smart twitter users and summarise the content. Time spent on running the code and getting output should be < 5 mins. 

## Data collection
There are multiple methods to scrape data from a public website including python libraries e.g. `BeautifulSoup`, `Requests`, and APIs offered by the platform. I understand Twitter has implemented some measures to deter web scraping so I expect some of these methods would be more difficult to implement. I did not want to use their API as it was not completely free to use so I explored varius turorials and eventually landed on [this one](https://www.freecodecamp.org/news/python-web-scraping-tutorial/) that introduced `Tweepy` and `Snscrape`. 

Using the `Snscrape` library, I gather a dataset of the following:
1. <b>Username</b> - Twitter handle
2. <b>DateCreated</b> - Date and time tweet was created
3. <b>NumberOfLikes</b> - Number of likes the tweet received
4. <b>NumberOfUsersQuotedTweet</b> - Number of times the tweet was quoted
5. <b>TweetRendered</b> - Tweet content (I use tweet.renderedContent instead of tweet.rawContent to retain any original url addresses which may provide a little more information then the urls customised by Twitter)

There are also [other attributes](https://thetechrobo.ca/snscrape-docs/_autosummary/snscrape.modules.twitter.Tweet.html#snscrape.modules.twitter.Tweet)  to explore, if interested.

!!Snscrape was blocked by Twitter and the kind developer who built it mentioned in some discussion thread that he would not be updating it soon so I resorted to using `Selenium` in a manual flow.!!

## Data processing
The dataset was filtered by date tweet was created from a week before to current day (UTC).

## Modelling
I simply asked ChatGPT to "Write a simple code using openai api to summarise a corpus" and "how to improve accuracy of the output", then used ChatGPT's recommendation to summarise the dataset. See our [conversation](https://chat.openai.com/share/7dc71458-ee07-43db-9327-96d0a4fa2ae2). 


## Limitations
There may be missed opportunites from the following:
- ChatGPT can make mistakes. If you took a close look at the suggested code, you'd see that it included duplicate `temperature` attribute which threw an error. I have not taken a detailed looked into the API to understand the available attributes and how the model can be better tuned.
- Using openai API is like using a blackbox i.e. despite using the `text-davinci-003` model, I am only aware that is is a pre-trained transformer neural network model and am unclear of the mechanisms.
The proof of this is in copying the corpus and [pasting into ChatGPT and asking for a summary](https://chat.openai.com/share/173f4b86-0f33-41d5-824e-073e1ef0f887). The output will be different and may be considered more/ less accurate.
- I also did not do any data cleaning to remove punctuations, links etc.. This may affect the accuracy of the output.
