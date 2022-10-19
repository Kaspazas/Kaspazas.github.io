---
title: Sentiment analysis
name: Sentiment analysis
layout: page
desc: Application of sentiment analysis to textual data
---
Sentiment analysis is a method of detecting emotions, affect and positivity/negativity in text. The form of sentiment analysis I'm familiar with is a dictionary based approach, wherein many words in a given language are rated by humans for positivity/negativity. For example, _satisfied_, while positive, is less positive than _happy_.

<h2>Example of implementation</h2>
Following the collection of 200,000 Reddit comments from /r/UkrainianConflict. The textual data has to be imported and pre-processed:

	data = pd.read_parquet('C:\\Users\\Kasparas Jucaitis\\Desktop\\portfolio\\Methods\\uacon_data.pq')

	data = data[data["moderator_status"] != "moderator"] #if moderator - at least 99% of mod posts are the intro comment
	data = data[data["text"] != ""] #if blank
	data = data[data["text"] != "[deleted]"] #if [deleted]
	data = data[data["text"] != "[removed]"] #if [removed]
	data["text"] = data["text"].str.lower() #lowercase the text

	for comment in data["text"]:
		comment = remove_emoji(comment) #note that the function is excluded due to lenght
		comment = re.sub(r'\w+:\/{2}[\d\w-]+(\.[\d\w-]+)*(?:(?:\/[^\s/]*))*', '', comment)
		comment = re.sub(r'/', '', comment)


I then use [VADER](https://github.com/cjhutto/vaderSentiment) to detect sentiment, specifically looking at the compound (overall) sentiment values:

	#create Sentiment analysis function
	analyzer = SentimentIntensityAnalyzer()
	def vadersentimentanalysis(text):
		sentiment = (analyzer.polarity_scores(text))
		return sentiment

	#Apply sentiment analysis function to text
	data["sentiment"] = data["text"].apply(vadersentimentanalysis)

Lastly, a bit of organization:

	#Reorganizing columns
	data = pd.concat([data, data["sentiment"].apply(pd.Series)], axis=1)
	data = data.drop(columns="sentiment")

	#Datetime conversion and index setting
	timeline = pd.DataFrame(data["created_utc"])
	i = 0
	while i < len(timeline):
		timeline.iloc[i,0] = datetime.fromtimestamp(timeline.iloc[i,0])
		i += 1

	#creating a dataframe that includes columns/variables of interest
	ua_con = pd.DataFrame([data["score"],data["comment_id"],data["compound"], data["text"]]).transpose()  # save all rows with 'human' in class column separately
	ua_con = ua_con.set_index(timeline.iloc[:,0])
	ua_con = ua_con.loc['2022-02-24' : '2022-07-29'] #sets dates
	del data, timeline #removes loaded dataframes to save ram

And then one is ready to evaluate and even visualize the sentiment of the entire dataset:
	
	ua_con.describe()
	
	ua_con_g = ua_con.groupby(pd.Grouper(freq='1440T')).mean()
	plt.plot(ua_con_g.index, ua_con_g.iloc[:,1])
	plt.title("Compound sentiment over time")
	plt.grid('both')

![sentiment whole](/assets/images/s_a1.png)

<h3>A deeper, more practically applicable approach</h3>
One can sub-divide devide their dataset, based on the topic of given texts, or through the inclusion of certain keywords.

For marketing, this could be used to examine sentiments related to features of a product or event. For example, one could evaluate the sentiment related to the price of a product, by segmenting the downloaded text into a sub-set that includes price related keywords. Note that this is a very basic approach, which can be improved through additional language processing (for example finding what words represent combined concepts through [word embedding](/methods/word-embedding) and more carefully defined queries.

As for the example dataset used here, we can use it to evaluate sentiment related to russian equipment:

	ru_weapons_split = pd.DataFrame()
	i=0
	while i < len(ua_con):
		for sentence in ua_con.iloc[i,3].split("."):
			if "russian" in sentence or "rus" in sentence or "vdv" in sentence or "wagner" in sentence or "kremlin" in sentence:
				if "weapons" in sentence or "tanks" in sentence or "rockets" in sentence or "uav" in sentence or "tanks" in sentence or "missiles" in sentence or "planes" in sentence:
					temp = pd.DataFrame([ua_con.iloc[i, :2]])
					temp["sentence"] = sentence
					ru_weapons_split = pd.concat([ru_weapons_split, temp])
		i+=1

	ru_weapons_split_sen = pd.DataFrame([vadersentimentanalysis(text) for text in (ru_weapons_split.iloc[:,2])])
	ru_weapons_split["compound"] = list(ru_weapons_split_sen.iloc[:,3])
	del ru_weapons_split_sen
	print("mean sentiment of sentences including russian equipment is: ", ru_weapons_split.iloc[:,3].mean())

	ru_weapons_split_sen = ru_weapons_split.groupby(pd.Grouper(freq='48H')).mean()
	plt.plot(ru_weapons_split_sen.index, ru_weapons_split_sen.iloc[:,1])

	>> mean sentiment of sentences including russian equipment is: -0.25

This code also returns a graph of sentiment over time, where the every value presented is an average of 48H worth of sentiment:

![sentiment ru_arms](/assets/images/s_a2.png)

The same can be done with sentences mentioning both Ukrainian armed forces and equipment. This does return a less negative mean sentiment of -0.23. Furthermore, the sentiments related to each nations military equipment can be graphed at the same time:

	plt.plot(ua_weapons_split_sen.index, ua_weapons_split_sen.iloc[:,1],'b',
         ru_weapons_split_sen.index, ru_weapons_split_sen.iloc[:,1],'r',)
	plt.grid('both')
	
![sentiment both arms](/assets/images/s_a3.png)

Note that the sub-reddit is generally pro-Ukrainian, so the sentiment recorded migh be reflecting comments such as these ones:

|     Example comments                                                                      |  Compound sentiment value |
|-------------------------------------------------------------------------------------------|---------------------------|
|_berlin blocked spain from sending german made tanks to ukraine_                           | -0.37                     |
|_it helps when the ukrainian precision weapons can target them but they can't target back_ | -0.038                    |

While some comments report a negative sentiment, they are often pro-Ukraine and generally praise Ukraine's weapons/their use.

<h2> Incomplete </h2>

Such an approach allows one to look for shifts in sentiment following major events.

