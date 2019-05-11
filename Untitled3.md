

```python
import sys
import csv
import tweepy
import tweepy
```


```python
#Change the x for your own API key.
consumer_key = "xxxxxxxxxxxxxxxxxxxx"
consumer_secret = "xxxxxxxxxxxxxxxxxxxxxx"
access_key = "xxxxxxxxxxxxxxxxxxxxxxxx"
access_secret = "xxxxxxxxxxxxxxxxxxxxxxx"

```


```python
def get_tweets(username):
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_key, access_secret)
    api = tweepy.API(auth)
```


```python
#Change 150 for the number of tweets you need.
    number_of_tweets = 150
```


```python
    tweets_for_csv = []
    for tweet in tweepy.Cursor(api.user_timeline, screen_name = username).items(number_of_tweets):
        tweets_for_csv.append([username, tweet.id_str, tweet.created_at, tweet.text.encode("utf-8")])
```


```python
    outfile = username + "_tweets.csv"
    print ("writing to " + outfile)
    with open(outfile, 'w+') as file:
        writer = csv.writer(file, delimiter=',')
        writer.writerows(tweets_for_csv)
```


```python
if __name__ == '__main__':

    if len(sys.argv) == 2:
        get_tweets(sys.argv[1])
    else:
        print ("Error: enter one username")
```
