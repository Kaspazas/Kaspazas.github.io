---
title: Twitter Bot Tactics
name: test_bots
layout: page
desc: Masters thesis on Twitter-bot behavior
---
In the thesis, I set out to discover patterns of Twitter bot behavior by comparing them to regular (human) users. To keep the work topical and allow for new insights outside of bot tactics, the Tweets collected were from Covid-vaccine related discussions on Twitter. Several informed assumptions lay at the foundation of this work. Firstly, bots, having been used by various actors for over 10 years, have likely undergone some form of optimization. Automated accounts comprise Twitter user populations at high rates. It is suggested that having portions of a botnet behave in slightly different ways is a plausible mechanism for over time optimizing outreach, garnering interactions and so forth. Secondly, while it was outside of the scope of this work to identify the deployers of these bots, it was assumed that most automated accounts detected were part of a broader information operation. In turn, this was used to inform the hypotheses developed for this work, wherein expected bot behaviors were derived from information warfare literature. As was found later, many bots retweeted each other at extremely high rates, supporting the idea that many of these users came from a single deployer. 

To ensure valid findings, I prioritized statistical comparisons where available. Drawing concrete conclusions only in cases where statistically significant differences could be observed between groups. Furthermore, I divided the category of “bot” into two: simple bots and sophisticated bots, based on prior research highlighting differences in behaviors based on bot-checker (in this case, Botometer LINK) score. Wherein a high bot-checker score indicates a type of automation that matches more with known bot behaviors, and less with known human behaviors, leading to the simple classification. A lower, but still high score is indicative of behaviors between that of known humans and bots, reflecting the sophisticated (more natural, human like) aspect of the second bot classification. I believe this differentiation to be meaningful and allowing for a more accurate understanding of the issues plaguing our social media. 

<h2>General observations</h2>
Data overview:

|                  |Tweets (% total)|Users (% total)|Initiated Retweets(% total)|Hashtags used (% total)|
|==================|================|===============|===========================|=======================|
|Simple bots       |3,673 (12.40%)  |2,418 (10.65%) |3,006 (16.49%)             |3,496 (14.53%)         |
|Sophisticated bots|2,807 (9.48%)   |1,764 (7.77%)  |1,872 (10.27%)             |3,821 (15.88%)         |
|Humans            |23,074 (77.92%) |18,471 (81.36%)|13,345 (73.23%)            |16,690 (69.37%)        |
|Total             |29,613          |22,703         |18,224                     |24,060                 |

Users that could not be classified (no Botometer score was returned) are included in totals.
The number of bots in the total population found in this work fall within expected numbers based on past works. Furthermore, matching past findings, both types of bots tend to tweet much more frequently than humans. This is indicated by the ratio of users to tweets.
Furthermore, an extremely high rate of hashtag use by sophisticated bots was observed.


Inter-class retweet rates:
|                |From Human              |From Simple            |From Sophisticated    |
|================|========================|=======================|======================|
|To Human        |10,218 (84.25% of total)|1,218 (42.88% of total)|1183 (67.41% of total)|
|To Simple       |983 (8.11 % of total)   |920 (32.39% of total)  |261 (14.87% of total) |
|To Sophisticated|927 (7.64% of total)    |702 (24.72% of total)  |311 (17.72% of total) |

As seen in the table above, simple bots tend to retweet other bots at extremely high rates compared to human users, indicating that they are likely aware of other bots in the discussion network their role is partly based on amplifying bot posted content. 

<h2>Network analysis</h2>
Visualization of the retweet network:
![old network image](/assets/images/network_temp.png)


The number of users per class amongst top performers for various network influence and centrality measures:

|     Measure                      |     Class            |     %   in top 100    |     %   in top 50    |     %   in top 15    |
|----------------------------------|----------------------|-----------------------|----------------------|----------------------|
|     Betweenness    centrality    |     Humans           |     70                |     62               |     86.67            |
|                                  |     Simple           |     21                |     22               |     0                |
|                                  |     Sophisticated    |     9                 |     16               |     13.33            |
|     Eigenvector centrality       |     Humans           |     69                |     68               |     66.67            |
|                                  |     Simple           |     11                |     12               |     13.33            |
|                                  |     Sophisticated    |     10                |     10               |     13.33            |
|     PageRank                     |     Humans           |     71                |     68               |     66.67            |
|                                  |     Simple           |     11                |     8                |     13.33            |
|                                  |     Sophisticated    |     8                 |     10               |     13.33            |
|     Authority                    |     Humans           |     72                |     74               |     80               |
|                                  |     Simple           |     9                 |     8                |     6.67             |
|                                  |     Sophisticated    |     8                 |     6                |     6.67             |
|     Hub                          |     Humans           |     63                |     56               |     40               |
|                                  |     Simple           |     18                |     20               |     33.33            |
|                                  |     Sophisticated    |     19                |     24               |     26.67            |

The thesis featured network analysis, wherein several network centrality and influence measures were calculated. The table above shows what percentage of each class comprised the lists of top-100,50,15 ranking users. 

Both classes of bots are seen to be over represented across most measures, given how many of the total users they comprise (wherein simple bots are x, sophisticated bots are y of the whole population). Sophisticated bots perform the best of all classes. As indicated by the number of these bots amongst top performing Eigenvector centrality and PageRank users, they are able to retweet and receive retweets from other influential users. 

Furthermore, inter-bot cooperation was observed in the dataset, the highest scoring sophisticated bot for PageRank (number 10 overall) received 55.07% of their retweets from simple bots, 10.52% from other sophisticated bots, and only 34.42% from humans. However, such disproportionate numbers of bot retweets are not found in many places throughout the dataset. The second-best performing bot under the PageRank measure received 65.82% of their retweets from humans, followed by 18.37% and 15.82% from simple and sophisticated bots respectively. Such rates of bot retweets were common for both bots and humans. 


<h2>Topic modelling</h2>

Using LDA (Latent Dirichlet Allocation via [Gensim](https://radimrehurek.com/gensim/)) there were a total of 13 topics found in the dataset. Note that applying topic modelling to Twitter posts and especially with a dataset of this size, does not yield the best results. Unfortunately, the procedure was already set upon realizing this. 

|     LDA label    |     Topic   name                                |
|------------------|-------------------------------------------------|
|     0            |     False   information                         |
|     1            |     Spread of Omicron                           |
|     2            |     Questioning   medical authorities           |
|     3            |     Mask wearing                                |
|     4            |     Poor   critical thinking ability            |
|     5            |     Non-vaccinated people causing   deaths      |
|     6            |     Antivax   beliefs                           |
|     7            |     Non-vaccinated people causing   deaths      |
|     8            |     Hospital   bed/ procedure unavailability    |
|     9            |     Freedom versus public health                |
|     10           |     Australia   and Djokovic                    |
|     11           |     Addressing antivaxxers                      |
|     12           |     Drinking   urine                            |


![participation across topics](/assets/images/thesis_1.png)

In this work, bots tended to avoid discussing the difficulties faced by the healthcare sector, the spread of the new (at the time of data collection) strain of COVID-19, mask wearing and the beliefs held by those considered antivax. As for the topics favored by bots in this work: the proliferation of false information, poor critical thinking ability and how to deal with antivaxxers in public policy or interaction.

<h2>Sentiment</h2>

The thesis also used sentiment analysis (via [VADER](https://github.com/cjhutto/vaderSentiment)) to observe the use of emotions by bots and humans. Based on the literature review, it was hypothesized that bots would have a significantly different, specifically lower average sentiment. 
In the thesis I divided the duration of the dataset into four segments (three 24h and one 12h periods) for which the sentiment between classes was compared statistically. 

![sentiment over time](/assets/images/thesis_2.png)
Because sentiment values as derived via [VADER](https://github.com/cjhutto/vaderSentiment) were not normally distributed, a limited selection of statistical tests remained valid. This work used Kruskal-Wallis H tests, which showed a significant difference in sentiment between user classes on three occasions. The segments with significant difference were: January 10th to January 11th (H(2) = 14.80, p = 0.0006), January 11th to January 12th (H(2) = 57.81 , p < 0.0001) and January 12th 12AM to January 12th 12PM (H(2) = 109 ,  p < 0.0001).

![class sentiments across topics](/assets/images/thesis_3.png)
As found via Dunn tests following initial Kruskal-Wallis H tests, humans and simple bots had significantly different sentiment in their tweets across nine topics (all but topics 3, 8, 10 and 12). Sophisticated bots differed from humans in six topics (namely topics 0, 1, 3, 4, 5 and 9). Only on one occasion where a significant difference was observed between sophisticated bots and humans, no significance (wherein p < 0.05) was present between the compound sentiments of simple bots and humans. Lastly, sophisticated bots differed from their simple counterparts on 4 occasions (topics 2, 4, 5 and 9).

<h2>Hashtags</h2>

![trumpvirus use per classification](/assets/images/thesis_4.png)

<h2>Main takeaways</h2>

1. A greater portion of simple bot retweets is directed toward other simple bots. It is posed by this work that this indicates an attempt to distort the discursive space by making it so that when human users seek out a topic on Twitter, much of the conversation will be occupied by tweets of bot-origin. Because simple bots do not retweet and thus directly interact with human users frequently (relative to other classes), they are likely being used to reinforce the appearance of discourse, ensuring that certain topics remain visible and salient.
2. It is posed that sophisticated bots target human users as interaction partners frequently and in turn, are able to better position themselves in a discursive network, reaching more important humans at higher rates. Furthermore, the thesis suggests that the benefit of sophisticated bots is also likely to be found in the content they produce, which is often liked and shared by humans.
3. Sentiment and content analyses show that while bots exhibit different preferences for sentiment and topics than humans, no clear patterns indicative of tactics can be identified in this work. This work did find that across most topics and timeframes, the sentiment between simple bots and humans was significantly different, indicating that simple bots construct/select the texts of their tweets in a way distinct to humans. Fewer instances of divergence were observed between sophisticated bots and humans, reinforcing XXX
4. Results relating to topic preferences did not reveal generalizable differences between the two types of automated accounts. Differences in participation across topics were found, but topics prioritized by either class did not seem to share any themes. In this work sophisticated bots, relative to simple bots (but not human users) were over represented in: Questioning medical authorities, Mask wearing and Unvaccinated people causing deaths. Simple bots participated in Spread of Omicron, Poor critical thinking ability and Addressing antivaxxers at higher relative rates than sophisticated bots. 
5. Both classes of automated accounts shared their compound sentiment valence across observed time segments, but the differences in intensity led to an identifiable significant difference in compound sentiment values for half of the occasions. These observations imply that the differences in sophistication should be informing sentiment-related hypotheses.





