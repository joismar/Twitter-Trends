# Projeto Twitter Trends - Disciplina de Programação 1

## Descrição
Primeiro projeto Python realizado com a ajuda da disciplica de Programação 1 do curso de Sistemas de Informação da UFPE. 
O projeto tinha o objetivo de com base em uma grande lista de twitts norte americanos, fazer uma análise de sentimentos e trazer diferentes resultados com base na análise. 
Mostrando eles em um mapa colorido de acordo com os sentimentos.

Segue abaixo todo o código proposto para ser escrito com base em um [modelo de projeto](https://github.com/joismar/Twitter-Trends/blob/master/trends_todo.py):

O resultado final pode ser visto [aqui](https://github.com/joismar/Twitter-Trends/blob/master/trends.py)

```python
def tweet_words(tweet):
    """Return a list of the words in the text of a tweet."""
    "*** YOUR CODE HERE ***"

def tweet_time(tweet):
    """Return the datetime that represents when the tweet was posted."""
    "*** YOUR CODE HERE ***"

def tweet_location(tweet):
    """Return a position (see geo.py) that represents the tweet's location."""
    "*** YOUR CODE HERE ***"
    
def extract_words(text):
    """Return the words in a tweet, not including punctuation.
    >>> extract_words('anything else.....not my job')
    ['anything', 'else', 'not', 'my', 'job']
    >>> extract_words('i love my job. #winning')
    ['i', 'love', 'my', 'job', 'winning']
    >>> extract_words('make justin # 1 by tweeting #vma #justinbieber :)')
    ['make', 'justin', 'by', 'tweeting', 'vma', 'justinbieber']
    >>> extract_words("paperclips! they're so awesome, cool, & useful!")
    ['paperclips', 'they', 're', 'so', 'awesome', 'cool', 'useful']
    """
    "*** YOUR CODE HERE ***"
    return text.split()  # Replace

def make_sentiment(value):
    """Return a sentiment, which represents a value that may not exist.
    >>> s = make_sentiment(0.2)
    >>> t = make_sentiment(None)
    >>> has_sentiment(s)
    True
    >>> has_sentiment(t)
    False
    >>> sentiment_value(s)
    0.2
    """
    assert value is None or (value >= -1 and value <= 1), 'Illegal value'
    "*** YOUR CODE HERE ***"

def has_sentiment(s):
    """Return whether sentiment s has a value."""
    "*** YOUR CODE HERE ***"

def sentiment_value(s):
    """Return the value of a sentiment s."""
    assert has_sentiment(s), 'No sentiment value'
    "*** YOUR CODE HERE ***"
    
def analyze_tweet_sentiment(tweet):
    """ Return a sentiment representing the degree of positive or negative
    sentiment in the given tweet, averaging over all the words in the tweet
    that have a sentiment value.
    If no words in the tweet have a sentiment value, return
    make_sentiment(None).
    >>> positive = make_tweet('i love my job. #winning', None, 0, 0)
    >>> round(sentiment_value(analyze_tweet_sentiment(positive)), 5)
    0.29167
    >>> negative = make_tweet("Thinking, 'I hate my job'", None, 0, 0)
    >>> sentiment_value(analyze_tweet_sentiment(negative))
    -0.25
    >>> no_sentiment = make_tweet("Go bears!", None, 0, 0)
    >>> has_sentiment(analyze_tweet_sentiment(no_sentiment))
    False
    """
    average = make_sentiment(None)
    "*** YOUR CODE HERE ***"
    return average


# Phase 2: The Geometry of Maps

def find_centroid(polygon):
    """Find the centroid of a polygon.
    http://en.wikipedia.org/wiki/Centroid#Centroid_of_polygon
    polygon -- A list of positions, in which the first and last are the same
    Returns: 3 numbers; centroid latitude, centroid longitude, and polygon area
    Hint: If a polygon has 0 area, return its first position as its centroid
    >>> p1, p2, p3 = make_position(1, 2), make_position(3, 4), make_position(5, 0)
    >>> triangle = [p1, p2, p3, p1]  # First vertex is also the last vertex
    >>> find_centroid(triangle)
    (3.0, 2.0, 6.0)
    >>> find_centroid([p1, p3, p2, p1])
    (3.0, 2.0, 6.0)
    >>> find_centroid([p1, p2, p1])
    (1, 2, 0)
    """
    "*** YOUR CODE HERE ***"

def find_center(polygons):
    """Compute the geographic center of a state, averaged over its polygons.
    The center is the average position of centroids of the polygons in polygons,
    weighted by the area of those polygons.
    Arguments:
    polygons -- a list of polygons
    >>> ca = find_center(us_states['CA'])  # California
    >>> round(latitude(ca), 5)
    37.25389
    >>> round(longitude(ca), 5)
    -119.61439
    >>> hi = find_center(us_states['HI'])  # Hawaii
    >>> round(latitude(hi), 5)
    20.1489
    >>> round(longitude(hi), 5)
    -156.21763
    """
    "*** YOUR CODE HERE ***"


# Phase 3: The Mood of the Nation

def find_closest_state(tweet, state_centers):
    """Return the name of the state closest to the given tweet's location.
    Use the geo_distance function (already provided) to calculate distance
    in miles between two latitude-longitude positions.
    Arguments:
    tweet -- a tweet abstract data type
    state_centers -- a dictionary from state names to positions.
    >>> us_centers = {n: find_center(s) for n, s in us_states.items()}
    >>> sf = make_tweet("Welcome to San Francisco", None, 38, -122)
    >>> ny = make_tweet("Welcome to New York", None, 41, -74)
    >>> find_closest_state(sf, us_centers)
    'CA'
    >>> find_closest_state(ny, us_centers)
    'NJ'
    """
    "*** YOUR CODE HERE ***"

def group_tweets_by_state(tweets):
    """Return a dictionary that aggregates tweets by their nearest state center.
    The keys of the returned dictionary are state names, and the values are
    lists of tweets that appear closer to that state center than any other.
    tweets -- a sequence of tweet abstract data types
    >>> sf = make_tweet("Welcome to San Francisco", None, 38, -122)
    >>> ny = make_tweet("Welcome to New York", None, 41, -74)
    >>> ca_tweets = group_tweets_by_state([sf, ny])['CA']
    >>> tweet_string(ca_tweets[0])
    '"Welcome to San Francisco" @ (38, -122)'
    """
    tweets_by_state = {}
    "*** YOUR CODE HERE ***"
    return tweets_by_state

def most_talkative_state(term):
    """Return the state that has the largest number of tweets containing term.
    >>> most_talkative_state('texas')
    'TX'
    >>> most_talkative_state('sandwich')
    'NJ'
    """
    tweets = load_tweets(make_tweet, term)  # A list of tweets containing term
    "*** YOUR CODE HERE ***"

def average_sentiments(tweets_by_state):
    """Calculate the average sentiment of the states by averaging over all
    the tweets from each state. Return the result as a dictionary from state
    names to average sentiment values (numbers).
    If a state has no tweets with sentiment values, leave it out of the
    dictionary entirely.  Do NOT include states with no tweets, or with tweets
    that have no sentiment, as 0.  0 represents neutral sentiment, not unknown
    sentiment.
    tweets_by_state -- A dictionary from state names to lists of tweets
    """
    averaged_state_sentiments = {}
    "*** YOUR CODE HERE ***"
    return averaged_state_sentiments


# Phase 4: Into the Fourth Dimension

def group_tweets_by_hour(tweets):
    """Return a dictionary that groups tweets by the hour they were posted.
    The keys of the returned dictionary are the integers 0 through 23.
    The values are lists of tweets, where tweets_by_hour[i] is the list of all
    tweets that were posted between hour i and hour i + 1. Hour 0 refers to
    midnight, while hour 23 refers to 11:00PM.
    To get started, read the Python Library documentation for datetime objects:
    http://docs.python.org/py3k/library/datetime.html#datetime.datetime
    tweets -- A list of tweets to be grouped
    """
    tweets_by_hour = {}
    "*** YOUR CODE HERE ***"
    return tweets_by_hour
```
