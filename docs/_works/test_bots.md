---
title: Twitter Bot Tactics
name: MA thesis on Twitter bots
layout: page
desc: Twitter bot behavior and tactics within COVID-19 vaccination related Twitter discourse
---

<h2>Introduction</h2>

In the thesis, I set out to discover patterns of Twitter bot behavior by comparing them to regular (human) users.
To keep the work topical and allow for new insights outside of bot tactics, the Tweets collected were from Covid-vaccine related discussions on Twitter.
Several informed assumptions lay at the foundation of this work. Firstly, bots, having been used by various actors for over 10 years, have likely undergone some form of optimization. Automated accounts comprise Twitter user populations at high rates. It is suggested that having portions of a botnet behave in slightly different ways is a plausible mechanism for over time optimizing outreach, garnering interactions and so forth. Secondly, while it was outside of the scope of this work to identify the deployers of these bots, it was assumed that most automated accounts detected were part of a broader information operation. 
In turn, this was used to inform the hypotheses developed for this work, wherein expected bot behaviors were derived from information warfare literature. As was found later, many bots retweeted each other at extremely high rates, supporting the idea that many of these users came from a single deployer.

<h3>The hypotheses: </h3>

The hypotheses were derived from a synthesis of academic literature covering information warfare, social media platform features, the types of action enabled by the design of bots and other literature featuring social psychology, persuasion and more.

Information warfare was used to identify broader approaches to controlling and exploiting the information environment of a given actor (group, state, etc.).
Through reviewing features and incentives of social media platforms, the thesis presented social media as a metaphorical _battleground_. Wherein network structures limit the ability of one to attack on a broad front, algorithms act as external forces that aid or hinder the spread of (dis)information, and the owners of the platforms get to alter the algorithmic forces or remove certain information/users, acting as a third party combatant. 
The technological features of bots show them to be a highly coordinated, easily replenishable force. In turn, these automated accounts, through their vast numbers can also shape the algorithms and make sure they infiltrate various corners of a discussion network.

Hypothesis 1-1: Bots will have a proportionately higher number of outgoing communications (tweets, retweets) than human accounts

Hypothesis 1-2: Bots with a higher Botometer score will retweet and mention other bots more frequently than sophisticated bots (accounts with lower Botometer scores)

Hypothesis 2: Bots will disproportionately occupy positions of high network influence

Hypothesis 3: Bots disproportionately participate in hostility inducing topics (e.g., insulting, stereotyping the opposition)

Hypothesis 4: Bots will disproportionately participate in conspiracy theory related topics

Hypothesis 5: The sentiment of bots will be significantly more negative than human sentiment

Hypothesis 6: Sentiment in bot tweets will be different from human sentiment for most subtopics

Hypothesis 7: Bots will participate in hashtag hijacking

<h4>Furthermore: </h4>

To ensure valid findings, I prioritized statistical comparisons where available. Drawing concrete conclusions only in cases where statistically significant differences could be observed between groups. Furthermore, I divided the category of “bot” into two: simple bots and sophisticated bots, based on prior research highlighting differences in behaviors based on bot-checker (in this case, [Botometer](https://botometer.osome.iu.edu/)) score. Wherein a high bot-checker score indicates a type of automation that matches more with known bot behaviors, and less with known human behaviors, leading to the simple classification. A lower, but still high score is indicative of behaviors between that of known humans and bots, reflecting the sophisticated (more natural, human like) aspect of the second bot classification. I believe this differentiation to be meaningful and allowing for a more accurate understanding of the issues plaguing our social media. 

Lastly, in the thesis and this write-up I refer to groups of users as a class (for classification), which are _missing_, _humans_, _simple bots_ and _sophisticated bots_, defined by [Botometer](https://botometer.osome.iu.edu/) scores.

<h2>General observations</h2>

Data overview:

|                  |Tweets (% total)|Users (% total)|Initiated Retweets (% total)|Hashtags used (% total)|
|==================|================|===============|============================|=======================|
|Simple bots       |3,673 (12.40%)  |2,418 (10.65%) |3,006 (16.49%)              |3,496 (14.53%)         |
|Sophisticated bots|2,807 (9.48%)   |1,764 (7.77%)  |1,872 (10.27%)              |3,821 (15.88%)         |
|Humans            |23,074 (77.92%) |18,471 (81.36%)|13,345 (73.23%)             |16,690 (69.37%)        |
|Total             |29,613          |22,703         |18,224                      |24,060                 |

Users that could not be classified (no [Botometer](https://botometer.osome.iu.edu/) score was returned) are included in totals.
The number of bots in the total population found in this work fall within expected numbers based on past works. Furthermore, matching past findings, both types of bots tend to tweet much more frequently than humans. This is indicated by the ratio of users to tweets.
Furthermore, an extremely high rate of hashtag use by sophisticated bots was observed.

Inter-class retweet rates:

|                             |     From   human                  |     From   simple bot            |     From   sophisticated bot    |
|-----------------------------|-----------------------------------|----------------------------------|---------------------------------|
|     To human                |     10,218   (84.25% of total)    |     1,218   (42.88% of total)    |     1183   (67.41% of total)    |
|     To basic bot            |     983 (8.11 % of total)         |     920 (32.39% of total)        |     261 (14.87% of total)       |
|     To sophisticated bot    |     927   (7.64% of total)        |     702   (24.72% of total)      |     311   (17.72% of total)     |

As seen in the table above, simple bots tend to retweet other bots at extremely high rates compared to human users, indicating that they are likely aware of other bots in the discussion network their role is partly based on amplifying bot posted content. 

<h4>Hypothesis 1-1 was confirmed because bots had rates (user to tweet) of out-going communications, which were higher than that of humans'</h4>
<h4>Hypothesis 1-2 was confirmed because both classes of bots (especially highlighted by simple bots) retweet other bots much more frequently than humans retweet bots</h4>

<h2>Network analysis</h2>

Visualization of the retweet network made using [Gephi](https://gephi.org/):
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

Both classes of bots are seen to be over represented across most measures, given how many of the total users they comprise (wherein simple bots are 10.65%, sophisticated bots are 7.77% of the whole population). Sophisticated bots perform the best of all classes. As indicated by the number of these bots amongst top performing Eigenvector centrality and PageRank users, they are able to retweet and receive retweets from other influential users. 

Furthermore, inter-bot cooperation was observed in the dataset, the highest scoring sophisticated bot for PageRank (number 10 overall) received 55.07% of their retweets from simple bots, 10.52% from other sophisticated bots, and only 34.42% from humans. However, such disproportionate numbers of bot retweets are not found in many places throughout the dataset. The second-best performing bot under the PageRank measure received 65.82% of their retweets from humans, followed by 18.37% and 15.82% from simple and sophisticated bots respectively. Such rates of bot retweets were common for both bots and humans. 

<h4>Hypothesis 2 was confirmed because bots comprised a disproportionate number of top-performing users across various influence and centrality measures</h4>

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

These are the sub-topics (and example tweets) relevant to the hypotheses:

|     Topic                                |     Example tweet                                                                                                                                                                                                                                                                                                |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     Spread of Omicron                    |     As the fake claim that ivermectin is a   miracle cure for COVID loses its shine, antivaxxers have turned to a new fake   claim. Apparently, omicron is now the miracle cure. A lot of filling   hospitals say otherwise.                                                                                     |
|     Addressing   antivaxxers             |     Macron   is right: It’s time to make life a living hell for anti-vaxxers!                                                                                                                                                                                                                                    |
|     Drinking Urine                       |     love that the antivaxxers have now   bent fully into the narrative that Jesus wants you to have a piss kink (???)                                                                                                                                                                                            |
|     Questioning medical   authorities    |     mRNA     The   vaccine works. There's been over 500 million doses. Its not experimental.   Doctors are smarter than you. The media that is being censored is being   censored because it is full of shit. The vaccine won't hurt you. Or kill you.        Stop   spreading propaganda. Idc if ur antivaxx    |
|     Antivax beliefs                      |     there is one pill that big   pharmaceutical will never produce or give to the people is truth.     #massformationpsychosis #pfizer   #astrazeneca #covid19 #holdtheline #antivaxx                                                                                                                            |

In this work, bots tended to avoid discussing the difficulties faced by the healthcare sector, the spread of the new (at the time of data collection) strain of COVID-19, mask wearing and the beliefs held by those considered antivax. As for the topics favored by bots in this work: the proliferation of false information, poor critical thinking ability and how to deal with antivaxxers in public policy or interaction.

![participation across topics](/assets/images/thesis_1.PNG)

Class participation rates in hostility inducing topics:

|     Sub-topic                  |     No. Humans        |     No. Simple bots    |     No. Sophisticated bots    |
|--------------------------------|-----------------------|------------------------|-------------------------------|
|     Spread of Omicron          |     1,092             |     109                |     80                        |
|     Addressing antivaxxers     |     825               |     285                |     138                       |
|     Drinking urine             |     212               |     30                 |     19                        |
|     Total ( % of all users)    |     2,129 (76.31%)    |     424 (15.2%)        |     237 (8.49%)               |

While bots (specifically simple bots) comprised a disproportionate number of users participating in hostility inducing topics, they did not do so outside of a confidence interval of 95%. Furthermore, some topics classified as hostility inducing, saw very few bots tweets. 

<h4>Hypothesis 3 was rejected because bots did not disproportionately contribute to hostility inducing topics</h4>

Class participation rates in conspiracy theory related topics:

|     Sub-topic                          |     No. Humans        |     No. Simple bots    |     No. Sophisticated bots    |
|----------------------------------------|-----------------------|------------------------|-------------------------------|
|     Questioning medical authorities    |     850               |     84                 |     83                        |
|     Antivax beliefs                    |     329               |     19                 |     28                        |
|     Total ( % of all users)            |     1,179 (84.64%)    |     103 (7.39%)        |     111 (7.94%)               |

Neither bot class showed disproportionate participation in conspiracy theory related topics, despite some these sub-topics containing actual instances of disinformation.

<h4>Hypothesis 4 was rejected because bots did not disproportionately participate in conspiracy-related discussions</h4>

<h2>Sentiment</h2>

The thesis also used sentiment analysis (via [VADER](https://github.com/cjhutto/vaderSentiment)) to observe the use of emotions by bots and humans. Based on the literature review, it was hypothesized that bots would have a significantly different, specifically lower average sentiment. 
In the thesis I divided the duration of the dataset into four segments (three 24h and one 12h periods) for which the sentiment between classes was compared statistically. 

![sentiment over time](/assets/images/thesis_2.PNG)
Because sentiment values as derived via [VADER](https://github.com/cjhutto/vaderSentiment) were not normally distributed, a limited selection of statistical tests remained valid. This work used Kruskal-Wallis H tests, which showed a significant difference in sentiment between user classes on three occasions. The segments with significant difference were: 

January 10th to January 11th (H(2) = 14.80, p = 0.0006);

January 11th to January 12th (H(2) = 57.81 , p < 0.0001);

January 12th 12AM to January 12th 12PM (H(2) = 109 ,  p < 0.0001).

<h4>Hypothesis 5 was rejected because despite bots having a significantly different sentiment than humans in most observed time periods, it was not significantly more negative overall</h4>

![class sentiments across topics](/assets/images/thesis_3.PNG)
As found via Dunn tests following initial Kruskal-Wallis H tests, humans and simple bots had significantly different sentiment in their tweets across nine topics (all but topics 3, 8, 10 and 12). Sophisticated bots differed from humans in six topics (namely topics 0, 1, 3, 4, 5 and 9). Only on one occasion where a significant difference was observed between sophisticated bots and humans, no significance (wherein p < 0.05) was present between the compound sentiments of simple bots and humans. Lastly, sophisticated bots differed from their simple counterparts on 4 occasions (topics 2, 4, 5 and 9).

<h4>Hypothesis 6 was confirmed because the sentiments of humans and bots were significantly different across most topics</h4>

<h2>Hashtags WORK IN PROGRESS</h2>

In the thesis, I tried to construct a custom methodology to detect hashtag hijacking, based on other works describing the phenomenon (namely [Prier, 2017](http://www.jstor.org/stable/26271634)).

The thesis considered a hashtag as being hijacked if:

1.	It was already actively being used by humans. 

2.	Bots start using the hashtag in disproportionate numbers.

3.	The hashtag’s meaning or associated discussion is altered once bots are introduced.


Out of the total 5022 unique hashtags contained in the dataset, 105 were used
prominently enough (exceeding 15 uses) by human users to be investigated further. Upon
graphing the usage of these by class, 13 showed enough sustained disproportionate use by bots to be considered as potentially being hijacked. That is,
these hashtags were being used at least once by bots for every two human uses and such a
ratio remained consistent for at least six hours.

Example of a hashtag meeting criterion 2:

![trumpvirus use per classification](/assets/images/thesis_4.PNG)

For criterion 3, to see if a hashtag's meaning or associated discussion is altered by the bots, the hashtags classified as potentially being hijacked had their associated tweet texts
examined via sentiment analysis, and compared between classes: 

![boxplots of sentiments](/assets/images/boxplots.png)

Due to the distribution of sentiments found in texts used alongside investigated hashtags, statistical tests could not be used to compare class sentiments, thus the thesis was limited to a visual comparison, and this method does not allow one to draw any concrete conclusions. Hence a follow up method was used.

Lastly, the frequencies of co-occurring (hashtags used in the same tweets as the investigated hashtag) were counted and compared between classes: 

|     Hashtag              |     Class     |     6 most used associated hashtags for both classes and number of respective co-occurrences.                           |
|--------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------|
|     urineidiot           |     Bots      |     antivaxxers: 89, qanons: 5, covidiots:   4, antivaxx: 3, urine: 3, urinetherapy: 2                                  |
|                          |     Humans    |     antivaxxers: 109,   urinetherapy: 18, covidiots: 17, covid19: 13, qanons: 11, antivaxx: 9                           |
|     unvaccinated*        |     Bots      |     antivaxx: 22, covid19: 21, quebec: 20,   healthtax: 20, qcpoli: 19, cdnpoli: 19                                     |
|                          |     Humans    |     antivaxxers: 43,   antivaxx: 33, covid19: 22, covidiots: 14, covid: 12, vaccineswork: 10                            |
|     vaccination          |     Bots      |     antivaxxers: 22, covid19: 10, cuban: 9,   deltavariant: 5, antivax: 5, covidvaccination: 4                          |
|                          |     Humans    |     antivaxxers: 42,   covid19: 33, antivax: 16, antivaxx: 13, mandatoryvaccination: 11,   vaxxedvsantivaxx: 11         |
|     trumpvirus           |     Bots      |     antivaxxers: 101                                                                                                    |
|                          |     Humans    |     antivaxxers: 48,   covid19: 3, unvaccinated: 3, covidiots: 2, desantis: 1, covid_19: 1                              |
|     quebec*              |     Bots      |     unvaccinated: 21, cdnpoli: 19, covid19:   18, qcpoli: 17, cdnhealth: 17, corona: 16                                 |
|                          |     Humans    |     antivaxxers: 21,   covid19: 11, antivaxx: 11, cdnpoli: 9, canada: 8, unvaccinated: 4                                |
|     freedom              |     Bots      |     antivaxx: 18, america: 15, antivaxxers:   5, humanrights: 2, novaccinemandates: 2, covid19: 2                       |
|                          |     Humans    |     antivaxx: 24, america:   19, antivaxxers: 8, antivax: 6, covid_19: 3, covid19: 3                                    |
|     science              |     Bots      |     antivaxxers: 9, climatechange: 5,   pandemicofselfoverothers: 5, antivax: 5, sciencedeniers: 5, deniers: 4          |
|                          |     Humans    |     antivaxxers: 33,   antivaxx: 11, covid19: 10, antiscience: 10, antivax: 10, climatechange: 6                        |
|     canada               |     Bots      |     antivaxxers: 10, unvaccinated: 8,   covid19: 8, quebec: 7, cdnpoli: 7, healthtax: 6                                 |
|                          |     Humans    |     antivaxxers: 20,   covid19: 13, antivaxx: 8, quebec: 8, unvaccinated: 7, cdnpoli: 7                                 |
|     america              |     Bots      |     antivaxx: 24, freedom: 15, antivaxxers:   6, antivax: 4, wwe: 3, maga: 3                                            |
|                          |     Humans    |     antivaxx: 29, freedom:   20, antivaxxers: 11, trump: 6, americafirst: 5, gop: 5                                     |
|     deltacron            |     Bots      |     covid19: 6, delta: 4, omicron: 3,   antivaxxers: 3, antivaxx: 2, pcrcollectsdna: 1                                  |
|                          |     Humans    |     covid19: 15,   antivaxxers: 9, omicron: 9, antivaxx: 6, vaccineswork: 4, omicronvariant: 4                          |
|     vaccine-mandates*    |     Bots      |     covid19: 22, antivaxx: 21,   coronavirusupdates: 20, qcpoli: 19, cdnpoli: 19, cdnhealth: 19                         |
|                          |     Humans    |     novaccinemandates: 31,   antivaxxers: 22, antivaxx: 15, covid19: 9, novaccinepassports: 8,   vaccinepassports: 5    |
|     funny*               |     Bots      |     jimmykimmel: 7, antivax: 7, hilarious:   7, barbie: 7, morningjoe: 7, tuesdayfunnies: 7                             |
|                          |     Humans    |     getvaccinated: 12,   wearamask: 12, humor: 9, comics: 9, antivax: 7, antivaxxers: 7                                 |
|     delta                |     Bots      |     covid19: 21, antivaxxers: 17,   deltavariant: 13, deltacron: 9, blog: 8, lifestyle: 8                               |
|                          |     Humans    |     covid19: 24, deltacron: 19, omicron: 18, antivaxxers: 17, antivaxx: 10, covidiots: 7                                |

Hashtags with an asterisk next to them (first column) show that over half of the most commonly co-occurring hashtags are different between classes. This indicates that associated discussion is different between bots and humans.

<h4> Hypothesis 7 was confirmed because several hashtags met the criteria of being hijacked </h4> 

<h4> BUT, </h4>
During the analysis procedures, many important faults were observed in the initially constructed method of detecting hashtag hijacking. 

<h2>Main takeaways</h2>

1. A greater portion of simple bot retweets is directed toward other simple bots. It is posed by this work that this indicates an attempt to distort the discursive space by making it so that when human users seek out a topic on Twitter, much of the conversation will be occupied by tweets of bot-origin. Because simple bots do not retweet and thus directly interact with human users frequently (relative to other classes), they are likely being used to reinforce the appearance of discourse, ensuring that certain topics remain visible and salient.

2. It is posed that sophisticated bots target human users as interaction partners frequently and in turn, are able to better position themselves in a discursive network, reaching more important humans at higher rates. Furthermore, the thesis suggests that the benefit of sophisticated bots is also likely to be found in the content they produce, which is often liked and shared by humans.

3. Sentiment and content analyses show that while bots exhibit different preferences for sentiment and topics than humans, no clear patterns indicative of tactics can be identified in this work. This work did find that across most topics and timeframes, the sentiment between simple bots and humans was significantly different, indicating that simple bots construct/select the texts of their tweets in a way distinct to humans. Fewer instances of divergence were observed between sophisticated bots and humans, reinforcing the idea that sophisticated bots behave and comunicate more like humans than simple bots.

4. Results relating to topic preferences did not reveal generalizable differences between the two types of automated accounts. Differences in participation across topics were found, but topics prioritized by either class did not seem to share any themes. In this work sophisticated bots, relative to simple bots (but not human users) were over represented in: Questioning medical authorities, Mask wearing and Unvaccinated people causing deaths. Simple bots participated in Spread of Omicron, Poor critical thinking ability and Addressing antivaxxers at higher relative rates than sophisticated bots. 

5. Both classes of automated accounts shared their compound sentiment valence across observed time segments, but the differences in intensity led to an identifiable significant difference in compound sentiment values for half of the occasions. These observations imply that the differences in sophistication should be informing sentiment-related hypotheses.





