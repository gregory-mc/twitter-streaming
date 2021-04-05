# Twitter Streaming

## NOTE: You need to get API KEYS first

### Description: 

This algorithm allows you to get tweets according to a word or tag, then tweets are saved in a database (SQLite) for your purposes

1. Define Twitter Listener: Here you choose how and which tweets are saved into database. I used just few parameters. You can check this in *[Tweepy Docs](https://docs.tweepy.org/en/latest/)*
~~~
class TweetsListener(tweepy.StreamListener):
~~~
2. Define API KEYS: You need to have these API KEYS, if you don't have them. Please, check this web: [Twitter](https://developer.twitter.com/en/docs/twitter-api)
3. DB Connection: I used SQLite but you can use any DB, just make sure you are using appropiate library to get connected to your database. You can use SQLAlchemy but you will have to add and change some lines of code.
~~~
con = sqlite3.connect("tweets.db") #database name
cursorObj = con.cursor()
cursorObj.execute("CREATE TABLE IF NOT EXISTS tweets(created date,user text, tweet text, user_name text,location text, retweets integer, likes integer)")
con.commit()
~~~
4. Streaming: 
~~~
stream = TweetsListener()
streamingApi = tweepy.Stream(auth=api.auth, listener=stream)
streamingApi.filter(track=['#DebatePresidencialJNE']) # Peruvian Subject
~~~
 You can change the word in *track* to find tweets about your subject
5. Final: I used pandas to read the data saved in the db but you can continue doing whatever you need. Pre processing, Spark, move to another database, etc.

