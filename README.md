# Covid-related tweets inside and outside China

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/d6d91258308f0908c5a399c88910caeff869bc95/Images/Network%20Science.png?raw=true)

Data has been collected from the following Twitter accounts:
- inside China: `CGTNOfficial`, `XHNews`
- outside China: `AJEnglish`, `AP`, `BBCWorld`,  `CNN`, `Reuters`

Periods of time for which data has been collected:
- from 22/01/2019 to 22/02/2019 -> early pandemic
- from 20/09/2020 to 21/10/2020 -> turning point of the epidemic and the serious controversy between Chinese and foreign media. At the UN General Assembly Trump criticized the Chinese government, and the Chinese media and the Ministry of Foreign Affairs refuted it. At the same time, China’s economy began to grow and became the only major economy in the world with positive growth.
- from 17/03/2021 to 17/04/2021 -> WHO released traceability report. CGTN and BBC reported the news about this report in different ways: CGTN said WHO said Wuhan was not the only possible Covid source, but BBC said Covid comes most likely from China. Also, during this time, China vaccine was reported not to work, but inside-China accounts may avoided to talk about that.

Keywords used to collect the data:
- first period -> `china`, `coronavirus`, `covid`, `wuhan`
- second period -> `china`, `coronavirus`, `covid`, `wuhan`, `vaccine`
- third period -> `covid`, `vaccine`, `WHO` (`delta` has been excluded)


## Exploratory Analysis

In order to try to get some insights about the collected data, we decided to perform an initial exploratory analysis.
This section is entirely dedicated to the presentation of the methods we used in order to extract information from the “China” and “outside China” tweets.
In particular, we did some exploratory analysis on the network using the main centrality measures.

The following is a log-log plot of the degree distribution of the two networks: the behaviour is almost equal in the two graphs, except for a small shift to the left of the China mean degree. It worths also noticing that for big enough degrees the two distributions follow a power law pattern.

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/e0c05830628538215f035f5ed3e9f0497b16bf57/Images/degree_distributions.png?raw=true)

In order to better understand the structure of the networks, we investigate its robustness capabilities. 
To do that we look at the behaviour of the number of connected components and of the size of the giant component under different nodes removal strategies, i.e. attacks:
• Random failure: we remove random nodes;
• Hubs removal: we remove the words with an higher degree first;
• Closeness removal: we remove the nodes with higher closeness centrality first;
• Betweenness removal: we remove the nodes with higher betweenness centrality first.

Inside China and Outside China networks behave in a similar way as described in the following figure.

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/3168c6707d1b34c549bb90b9e818faf038dde005/Images/A_T.png?raw=true)

In order to get some statistical significance from our analysis, we decided to test some probabilistic models that tries to capture the generative process behind the network itself. In particular, we tried p2-ergm and AME models.
After fitting the model on both of the networks, we compared additive effects for the highest common Pagerank nodes as shown in the following.

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/779ee67da35bab7c3e3d6d913b351621fc28d049/Images/additive_effects_ame.png?raw=true)

The next figure represents the “best superposition” of latent nodal representations of the highest Pagerank words in the two networks:

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/779ee67da35bab7c3e3d6d913b351621fc28d049/Images/latent_effects.png?raw=true)

Finally, we have a boxplot comparison of the amen-simulated PageRank marginal distribution for the highest PageRank words in the two networks:

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/779ee67da35bab7c3e3d6d913b351621fc28d049/Images/simulated_pr_usa.png?raw=true)


## Community Detection

We identify the hidden relationships that may exist among the nodes in a network, indicating communities of nodes. 
We implemented six different strategies to carry out the task: Kernighan–Lin bipartition, dendrograms, Clauset-Newman-Moore and Louvain method (modularity maximization) for discovering some relevant network partitions, while Big CLAM and Clique percolation for highlighting possibly overlapping communities.

The following are examples of community detection graphical representation:

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/29212b9b7dfdf89332fc3fcada2d82686137e2bf/Images/den-all.png?raw=true)

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/29212b9b7dfdf89332fc3fcada2d82686137e2bf/Images/China_louvain.png?raw=true)

In general, Clauset-Newman-Moore and the Louvain method find pretty similar communities: the number of communities may vary but, overall, the semantic content remains almost the same. We will leave out of the analysis some very small and not much interpretable communities. This kind of communities increases in number as we proceed from the earlier period to the later period: this could possibly mean that the Covid-19 debate was more polarized in some major topics during the January-February 2020 period, while getting more various and including much different topics in the March-April 2021 period. This is reasonable because at first the official channel news tended to report almost the same information about the health emergency, but as time passed they started to enrich and vary the content of their tweets.
The following table displays the communities detected with Modularity maximization methods on medium-size network referring to all the three selected periods together. 

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/ec7f5223092dc278e5bd746340393a96debd1bb9/Images/table.png?raw=true)

## Sentiment Analysis

We investigate the differences in the medias discussion (inside and outside China) based on the analysis of sentiment with the use of the LIWK software: we spot the difference in values of the markers tweets over the different time periods and compare through linear regression different marker.

The following image reports the following information: the variables negative emotions (a) and death (f) are much higher in the first period and tend to decrease in the following two periods. This trend may be due to the desire to reassure the population after the first period, in which panic broke out all over the world also because of the excessive amount of alarmist news. In addition the chinese media tends to write tweets containing more numbers (k). On the contrary, the variables empowerment (g), positive emotions (b) and affiliation (j) increase in the second two periods for tweets outside China, showing the desire to report the contingent situation as under control. These variables, for China’s tweets, are already very high in the first period, demonstrating (apparent) positivity and control even in a very critical moment. The most substantial differences are in the variables we (h) and they (i). The value of we is much higher in tweets from outside China for all three periods. The value of they, on the other hand, is much higher in tweets from China in the first period and then stabilises in subsequent periods.

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/667070856919bb1f86e9d41007b5f879dbc61df7/Images/bars.png?raw=true)

To further investigate the differences between tweets from inside and outside China, we analyzed the variables "we" and "they", which indicate belonging and distancing respectively, by associating them with the variables positive emotions and negative emotions. The following figure show the linear regression (with confidence intervals) of "they" versus "negemo" (the same has be done for "we" versus "posemo"), first considering all periods together and then dividing into the single periods. 
The they-negemo association appears much stronger inside China (considering the slope).

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/667070856919bb1f86e9d41007b5f879dbc61df7/Images/linreg.png?raw=true)

The following image show the 20 obtained words with higher projected Negative emotions during the first period on the left and the 20 words with higher m∗w on the right, inside (first row) and outside China (second row). For instance the words "bat", "soup", "goodwill". Those are all related with tweets that clearly aim to defend the
China from the "echoing" of being the source of Covid-19, "criticizing" the "unfriendly" U.S comments as not a sign of "goodwill".

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/667070856919bb1f86e9d41007b5f879dbc61df7/Images/clouds.png?raw=true)

The last figure compares the networks obtained by considering tweets inside and outside China separately, for each of the three selected periods.
The colour of each node represents the community it belongs to, while the size is directly proportional to the value assigned to each word by the projection algorithm.
For the first period, looking at tweets from Chinese news accounts (a), we see in the biggest community (purple) words such as "unfriendly", "bat", "criticize", "in-action", all of which are contained in tweets complaining about the behaviour of America, which spreads fake news and blames China for the pandemic. The orange community also reports Asian people being discriminated against and accused of carrying the virus to Europe. The green community with the words "crazy", "mourn" and "slander" contains words related to news that both describe as absurd the theory that the virus was created by China and mourn doctor Li Wenliang, a doctor who passed away after being infected with the coronavirus.
For tweets outside China (b), the word with the highest value is "flyer". When analyzing the news, we notice that this word often appears in news reporting that when
the pandemic broke out, flyers were distributed in California urging people not to go to Asian restaurants, blaming them for spreading the virus. This word belongs to a community (the purple one) in which also the other most important words are used in the same news or in news with different topics, all negatively related to China.

![alt text](https://github.com/silviapoletti/Covid19-related-tweets-Network-Analysis/blob/667070856919bb1f86e9d41007b5f879dbc61df7/Images/proj.png?raw=true)
