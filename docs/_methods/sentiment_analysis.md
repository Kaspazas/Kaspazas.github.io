---
title: Sentiment analysis
name: Sentiment analysis
layout: page
desc: Application of sentiment analysis to textual data
---
Sentiment analysis is a method of detecting emotions, affect and positivity/negativity in text. The form of sentiment analysis I'm familiar with is a dictionary based approach, wherein many words in a given language are rated by humans for positivity/negativity. For example, _satisfied_, while positive, is less positive than _happy_.

<h2>Example of implementation</h2>
Following the collection of 200,000 Reddit comments from /r/UkrainianConflict. The textual data had to be pre-processed:

	data = data[data["moderator_status"] != "moderator"] #if moderator - at least 99% of mod posts are the intro comment
    data = data[data["text"] != ""] #if blank
    data = data[data["text"] != "[deleted]"] #if [deleted]
    data = data[data["text"] != "[removed]"] #if [removed]
    data["text"] = data["text"].str.lower() _#lower case everything_
	uacon_texts = list(data["text"])
	
    uacon_comments = []
    for comment in uacon_texts:
        comment = re.sub(r'\w+:\/{2}[\d\w-]+(\.[\d\w-]+)*(?:(?:\/[^\s/]*))*', '', comment)
        comment = re.sub(r'/', '', comment)
        uacon_comments.append(comment)
    uacon_texts = uacon_comments

I then use [VADER](https://github.com/cjhutto/vaderSentiment) to detect sentiment:

	#create function
    analyzer = SentimentIntensityAnalyzer()
    def vadersentimentanalysis(text):
        sentiment = (analyzer.polarity_scores(text))
        return sentiment

	'uacon_texts = pd.DataFrame([[vadersentimentanalysis(text) for text in uacon_texts],uacon_texts])'


<h3>A deeper, more practically applicable approach</h3>
One can sub-divide devide their dataset, based on the topic of given texts, or through the inclusion of certain keywords.

For marketing, this could be used to examine sentiments related to features of a product or event. For example, one could evaluate the sentiment related to the price of a product, by segmenting the downloaded text into a sub-set that includes price related keywords.

As for the example dataset used here, we can use it to evaluate sentiment related to russian equipment:

    ru_weapons_split = []
    for comment in uacon_texts:
        for sentence in comment.split("."):
            if "russia" in sentence or "russian" in sentence or "wagner" in sentence or "vdv" in sentence:
                if "weapons" in sentence or "equipment" in sentence or "vechicles" in sentence or "tanks" in sentence or "planes" in sentence:
                    ru_weapons_split.append(sentence)
    
    'ru_weapons_split = pd.DataFrame([[vadersentimentanalysis(text) for text in ru_weapons_split],ru_weapons_split]).transpose()'
    'ru_weapons_split = pd.concat([ru_weapons_split, ru_weapons_split.iloc[:,0].apply(pd.Series)], axis=1)'
    'print("mean sentiment of sentences including russian arms is: ", ru_weapons_split.iloc[:,5].mean())'
	>> -0.24

<h2>Visualizations</h2>

