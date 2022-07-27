What Goes Into a Successful Reddit Post?
======================================
Here I'll pull and explore some data from Reddit

I'll attempt to find out what about a Reddit post makes it successful using classification. In particular a Random Forest model and KNNeighbors model.

Then I'll score the results and see what the highest predictors are

To find what goes into making a successful Reddit post we'll have to do a few things, first of which is collecting data:

## Introducing Scrapey!

[Scrapey](scrapey.ipynb) takes a snapshot of [Reddit/r/all hot](https://www.reddit.com/r/all), and saves the data to a .csv file including a calculated age for each post about every 12 minutes. Run time is about 2 minutes per iteration and each time adds about 100 unique posts to the list while updating any post it's already seen.

I run this in the background in a terminal and it updates my data set every ~12 minutes. I have records of all posts within about 12 minutes of them disappearing from /r/all.

## EDA
Chosen Features:
* Title
* Subreddit
* Over_18
* Is_Original_Content
* Is_Self
* Spoiler
* Locked
* Stickied
* Num_Comments (Target)

[EDA](EDA.ipynb)

## Clean
* Scale numeric features between 0-1
* Convert '_' and '-' to whitespace
* Remove any not a-z or A-Z or whitespace
* Strip any leftover whitespace
* Delete any titles that were reduced to empty strings

[Clean](clean.ipynb)

## Model
* Split data to train/test samples
* Test RandomForestClassifier, KNeighborsClassifier
* My preferred is RandomForest

[Model](model.ipynb)

### Conclusion

Long story short, if you want to karma farm then post OC memes and porn.

Some Predictors from Top 25:
* Is_Self
* Subreddit_Memes
* OC
* Over_18
* Subreddit_Shitposting
* Is_Original_Content
* Subreddit_Superstonk

Popular words: 

'like', 'just', 'time', 'new', 'oc', 'good', 'got', 'day', 'today', 'im', 'dont', and 'love'.

People on Reddit (at least in the past few days) like their memes, porn, and talking about their day. And it's preferred if the content is original and self posted.

So yes, post your memes to memes and shitposting, tag them NSFW, use some words from the list, and rake in all that sweet karma!

But it's not that simple, this is a fairly simple model, with simple data. To go beyond this I think the comments would have to be analyzed. Tokenization I thought would be the most influential piece, and I still think that thinking is correct. But in this case it doesn't apply because there is no real meaning to be had from reddit post titles, at least to a computer. There's a lot more seen by a human than just the text in the title, there's often an image attached, most posts reference a recent/current event, they could be an inside joke of sorts. For some posts there could be emojis in the title, and depending on their combination they can take on a meaning completely different from their individual meanings. 

The next step from here I believe is to analyze the comments section of these posts because in this moment I think that's the easiest way to truly describe the meaning of a post to a computer. With what was gathered here I'm only to get 10% above baseline and I think that's all there is to be had here, I mean we can tweak for a few percent probably but I don't think there's much left on the table.