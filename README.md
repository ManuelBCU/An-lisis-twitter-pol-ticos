# How did I do it?
## Spanish politicians Twitter accounts, a lexical analysis.
### This is the article: https://manuelbcu.github.io/An-lisis-twitter-pol-ticos/
Spain faces its 14th general elections on April 28. In this article I analyze the twitter account of the main candidates, locating the most treated topics over the campaign and finding the differences and similiarities in their discourses.

## Using the Twitter API to scrape tweets.

To access the Twitter information, the first thing you need is an API key. This will allow you to locate the tweets and extract them to analyze them. Getting an api key from Twitter is very [simple](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens.html) and you will need it to get access to Twitter information with your Python code. Once you have your key you can start writing your code.

## Writing the code on Python
To start writing the code on Python the first thing to do is installing the needed libraries. In this case, we are going to use sys, csv and tweepy. Tweepy is a very good library to scrape information from Twitter and it has a lot of different functions. In this case we are going to extract tweets and retweets, but if you need to do something else you can get all the information on its [website](https://www.tweepy.org/).

```python
import sys
import csv
import tweepy
```
Now you need to use the API key to acces the Twitter API.
```python
#Change the 'x' for your own API key.
consumer_key = "xxxxxxxxxxxxxxxxxxxx"
consumer_secret = "xxxxxxxxxxxxxxxxxxxxxx"
access_key = "xxxxxxxxxxxxxxxxxxxxxxxx"
access_secret = "xxxxxxxxxxxxxxxxxxxxxxx"
```
Creating the function to extract the tweets.
```python
def get_tweets(username):
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_key, access_secret)
    api = tweepy.API(auth)
```
Setting the number of tweets you want to get.
```python
#Change 150 for the number of tweets you need.
    number_of_tweets = 150
```
Getting the tweets.
```python
    tweets_for_csv = []
    for tweet in tweepy.Cursor(api.user_timeline, screen_name = username).items(number_of_tweets):
        tweets_for_csv.append([username, tweet.id_str, tweet.created_at, tweet.text.encode("utf-8")])
```
Setting the file to save the tweets.
```python
    outfile = username + "_tweets.csv"
    print ("writing to " + outfile)
    with open(outfile, 'w+') as file:
        writer = csv.writer(file, delimiter=',')
        writer.writerows(tweets_for_csv)
```
Running the tweets as a script.
```python
if __name__ == '__main__':

    if len(sys.argv) == 2:
        get_tweets(sys.argv[1])
    else:
        print ("Error: enter one username") 
```
## Running the code.
Once you have written the code. Go to **Command Prompt** and write: python   (the path to your file)   (the username of the account you want to scrape).
This is an example on how it looks like on my computer.
![alt tex](https://raw.githubusercontent.com/ManuelBCU/An-lisis-twitter-pol-ticos/master/Capture.JPG)
Now that you have done it you will have a csv file with the tweets you have scraped.

## Doing a lexical analysis.
Once I had all the files I separated them by month, as I wanted to analyze how some words have been used along the campaign. It is a very easy thing to do with **Excel** filters as with this code you get the time each tweet was published. I used Excel filters and separated them.  
For the lexical analysis I decided to use [Antconc](https://www.laurenceanthony.net/software/antconc/).  
This tool is available both for windows, mac and linux. It allows you to find parameters and list the words in a text file. The only thing you need to do is to get the data by month and put them on different **text files** to analyze them. 
Once I had all the word lists, I separated them by month and started to search for the most interesting parameters.

## Making it visual
For the images in the article I used **Adobe Photoshop**, choosing some of the words more repeated by each politician. I decided to use the Twitter blue colour code for both the images and the headings to give them the same style.
Finally, with the topics I found interesting I created different graphics with [Flourish](https://flourish.studio/) which is a very easy-to-use visualization tool. 
