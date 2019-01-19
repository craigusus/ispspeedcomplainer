# Speed Complainer
A python app that will test your internet connection and then complain to your service provider (and log to a data store if you'd like)

## Dependencies
```
sudo apt-get install python-pip

sudo pip install speedtest-cli daemon python-twitter
```

## Configuration
Configuration is handled by a basic JSON file. Things that can be configured are:
```
twitterToken: This is your app access token
twitterConsumerKey: This is your Consumer Key (API Key)
twitterTokenSecret: This is your Access Token Secret
twitterConsumerSecret: This is your Consumer Secret (API Secret)

tweetTo: This is a account (or list of accounts) that will be @ mentioned (include the @!)
internetSpeed: This is the speed (in Mbs) you're paying for. (Minimum Guaranteed Access Line Speed)
tweetThresholds: This is a list of messages that will be tweeted when you hit a threshold of crappiness. Placeholders are:
 {tweetTo} - The above tweetTo configuration.
 {internetSpeed} - The above internetSpeed configuration.
 {downloadResult} - The download speed you're getting
```

Threshold Example (remember to limit your messages to 140 characters or less!):
```
"tweetThresholds": {
        "14": [
            "Hey {tweetTo} I'm paying for {internetSpeed}Mbs but getting only {downloadResult}Mbs?!? Shame.",
            "Oi! {tweetTo} £50+/m for {internetSpeed}Mbs and I only get {downloadResult}Mbs? How does that seem fair?"
        ],
        "32": [
            "Uhh {tweetTo} for £50+/m I expect better than {downloadResult}Mbs when I'm paying for {internetSpeed}Mbs. Fix your network!",
            "Hey {tweetTo} why am I only getting {downloadResult}Mbs when I pay for {internetSpeed}Mbs? £50+/m for this??"
        ],
        "42": [
            "Well {tweetTo} I guess {downloadResult}Mbs is better than nothing, still not worth £50+/m when I expect {internetSpeed}Mbs"
        ]
    }
```

Logging can be done to CSV files, with a log file for ping results and speed test results.

CSV Logging config example:
```
"log": {
    "type": "csv",
    "files": {
        "ping": "pingresults.csv",
        "speed": "speedresults.csv"
    }
}
```

## Usage
> sudo python speedcomplainer.py

Or to run in the background:

> sudo python speedcomplainer.py > /dev/null &
